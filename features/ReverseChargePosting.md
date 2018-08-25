# Reverse Charge Posting

Reverse Charge VAT functionality enables posting of inbound and outbound VAT in Purchase documents, creating two separate VAT entries with two different VAT dates. Report Calc. and Post VAT Settlement is changed to support closing of two instead of only one entry and to take in account VAT receivables and payables account set in the report, instead of the reverse charge accounts set in VAT Posting Setup.

> Sanja: When reverse functionality is used, internal correction is set automatically. Table „Cancelled Document“, field  „Cancelation Doc. No.“ use to filter customer/vendor ledger entry. ???

## Scope

User must be able to enter VAT Output Date (this is the VAT Date when user needs to post VAT only). The entires must be in addition posted to VAT Entries. When posting document, two similar VAT Entries are created, one with Type Purchase and the other with Type Sales (negative amounts). VAT Output date is copied to VAT Entries to
VAT Date in the line with Type Sales.

User can enter VAT Output date in documents: Purchase Invoice, Purchase Order, Purchase
Return Order and Purchase Credit Memo, General Journal, Purchase Journal.

User can reverse posted transaction, which reverses all entries including Reverse Charge VAT
in 2 additional lines.

User can run report Calc. and Post VAT Settlement which closes both entries created based
on Reverse Charge VAT. Entries are closed not through Reverse Charge VAT from VAT Posting
Setup (standard functionality) but through Sales/Purchase Settlement Account defined on
request form of report.

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
Posting Date|Document Type|Output Date|VAT Date|VAT %|VAT Amount|VAT % (retrograde)
-:|-|-|-:|-:|-:|-:|-:|-:
20.08.18|Purchase Invoice||01.09.18|100|1.000,00|20

### VAT Entry - standard way
Posting Date|Amount|Base|Unrealized Amount|Unrealized Base|Remaining Amount|Remaining Base
-:|-:|-:|-:|-:|-:|-:
20.08.18|0,00|0,00|1.000,00|100.000,00|1.000,00|100.000,00

### VAT Entry - modified way
Posting Date|Amount|Base|Unrealized Amount|Unrealized Base|Remaining Amount|Remaining Base
-:|-:|-:|-:|-:|-:|-:|-:
01.09.18|0,00|0,00|1.000,00|20.000,00|0,00|0,00
30.08.18|1.000,00|20.000,00|0,00|0,00|0,00|0,00
01.09.18|-1.000,00|-20.000,00|0,00|0,00|0,00|0,00

## User Interface
VAT Output date in documents: Purchase Invoice, Purchase Order, Purchase Return Order and Purchase Credit Memo, General Journal, Purchase Journal.
