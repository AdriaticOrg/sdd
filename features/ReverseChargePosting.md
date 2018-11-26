# Reverse Charge Posting

Reverse Charge VAT functionality enables posting of inbound and outbound VAT in Purchase documents, creating two separate VAT entries with two different VAT dates that reflects in additional VAT Entries in Posting Date.

> Range: 13.062.525..13.062.550

## Scope

User must be able to enter VAT Output Date (this is the VAT Date when user needs to post VAT only). Entires must be in addition posted to VAT Entries. When posting document, two similar VAT Entries are created, one with Type Purchase and the other with Type Sales (negative amounts). VAT Output Date is copied to VAT Entries to Posting Date in the line with Type Sales.

User can enter VAT Output date in documents: Purchase Invoice, Purchase Order, Purchase Return Order and Purchase Credit Memo, General Journal, Purchase Journal.

User can reverse posted transaction, which reverses all entries including Reverse Charge VAT for additional line.

User can run report Calc. and Post VAT Settlement which closes both entries created based on Reverse Charge VAT. 

## Data Design

Added fields on purchase tables:

Type|Table|Field
-|-|-
Document|Purchase Header|VAT Output Date
Journal|Gen. Journal Line|VAT Output Date
Posted Document|Purch. Rcpt. Header|VAT Output Date
Posted Document|Purch. Inv. Header|VAT Output Date
Posted Document|Purch. Cr. Memo Hdr.|VAT Output Date

## Data Flow

New VAT Entry must be created first standard with Purchase Type and the other Sales Type.

Create new entry after posting original one. Information of document is stored in GenJnlLine.

``` PAS
Object TABLE 254 VAT Entry
    OnAfterCopyFromGenJnlLine(Rec,GenJnlLine);
``` 
### Sales or Purchase Document
Posting Date|Document Type|VAT Calculation Type|VAT Amount|VAT Base
-:|-:|-:|-:|-:
20.08.18|Purchase Invoice|Reverse VAT|200,00|1.000,00

### VAT Entry - standard way
Posting Date|Type|Amount|Base
-:|-:|-:|-:
20.08.18|Purchase|200,00|1.000,00

### VAT Entry - modified way
Posting Date|Type|Amount|Base
-:|-:|-:|-:
20.08.18|Purchase|200,00|1.000,00
20.08.18|Sale|200,00|1.000,00

## User Interface
VAT Output date in documents: Purchase Invoice, Purchase Order, Purchase Return Order and Purchase Credit Memo, General Journal, Purchase Journal.
