# Full VAT posting

Local full VAT posting functionality enables calculation of VAT base based on VAT Amount and VAT %, when VAT Calculation Type is set to Full VAT and allows user to change VAT base in Lines of Statistics on documents.

> Alias: VAT Base Retrograde

## Scope
User must be able to post Advanced Prepayment when payment is created in period before the goods or service are delivered.


## Data Design

Add fields to following tables:

Table|Field
-|-
VAT Posting Setup|VAT % (retrograde)
Gen. Journal Line|VAT % (retrograde)
VAT Entry|VAT % (retrograde)
VAT Entry|Vat Base Retro|

## Data Flow

### Copy

Copy value from Sales / Purchase Document to Gen. Journal Line. 
``` PAS
OBJECT Codeunit 80 Sales-Post 
    OnAfterPostInvPostBuffer(GenJnlLine,InvoicePostBuffer,SalesHeader,GLEntryNo); 
```
``` PAS
OBJECT Codeunit 90 Purch.-Post 
    OnAfterPostInvPostBuffer(GenJnlLine,InvoicePostBuffer,PurchHeader,GLEntryNo); 
```

### Posting

Create new codeunit Full VAT-Post and subscribe to event which is triggered when "VAT Entry" is created (posted). Calculate VAT Base Retro with following formula:

``` PAS
OBJECT Table 255 VAT Entry 
    OnAfterCopyFromGenJnlLine(Rec,GenJnlLine); 
    BEGIN
        "VAT Base Retro" := (Base + Amount) * 100 / "VAT Posting Setup"."VAT % (retrograde)";
    END;
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
Posting Date|Amount|Base|Unrealized Amount|Unrealized Base|Remaining Amount|Remaining Base|VAT Base Retro
-:|-:|-:|-:|-:|-:|-:|-:
20.08.18|1.000,00|20.000,00|1.000,00|20.000,00|0,00|0,00|20
01.09.18|0,00|0,00|-1.000,00|-20.000,00|1.000,00|20.000,00|20

## User Interface

"VAT Base Retro" should be available on Sales and Purchase documents and Gen. Journal Line for editing.