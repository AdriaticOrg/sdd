# Informative VAT

Informative VAT in Sales invoices functionality enables printing of VAT for informative purposes in accordance with the 76. Article of Slovenian Value Added Tax Act. In this case VAT is not calculated and posted, but only printed in two additional columns of VAT Amount Specification: Informative VAT % and Informative VAT amount.

> Range: 13.062.551..13.062.560

> Country: SI

## Scope

Use VAT % (informative) percentage to show on documents how much VAT would normally be calculated.

## Architectural Design 

Post transactions normally. Use VAT Amount Line table to express calculated VAT %. 
[Sales Documents](SalesDocuments.md) feature should print the VAT % (informative) value.

## Data Design

New fields: 

Table|Field|Type
-----|-----|----
VAT Posting Setup|VAT % (informative)|Decimal
VAT Amount Line|VAT % (informative)|Decimal
Sales Line|VAT % (informative)|Decimal
Sales Invoice Line|VAT % (informative)|Decimal
Sales Cr.Memo Line|VAT % (informative)|Decimal
Service Line|VAT % (informative)|Decimal
Service Invoice Line|VAT % (informative)|Decimal
Service Cr.Memo Line|VAT % (informative)|Decimal

> Note: Service module is not supported with appropriate events!

## Data Flow

Case for posting: 

VAT Bus. Posting Group|VAT Prod. Posting Group|VAT Calculation Type|VAT Identifier|VAT %|VAT % (Informative)
----------------------|-----------------------|--------------------|--------------|-----|-------------------
K-DA|B-22|Normal VAT|36|22|0
K-DA|B-9,5|Normal VAT|35|9,5|0
K-DA|ODB-22|Normal VAT|36|0|22
K-DA|ODB-9,5|Normal VAT|35|0|9,5

### Posting VAT Entry for Normal VAT %
Posting Date|Type|Amount|Base|VAT % 
-:|-:|-:|-:|-:
20.08.18|Sale|-220,00|-1.000,00|22

### Posting VAT Entry for Normal VAT % (Informative)
Posting Date|Type|Amount|Base|VAT %
-:|-:|-:|-:|-:
20.08.18|Sale|0,00|-1.000,00|0

Use following event from Sales Line Table.

``` PAS
LOCAL [IntegrationEvent] OnAfterCalcVATAmountLines(VAR SalesHeader : Record "Sales Header";VAR SalesLine : Record "Sales Line";VAR VATAmountLine : Record "VAT Amount Line";QtyType : 'General,Invoicing,Shipping');
```

> NOTE: Service Line does not have similar event. It should be requested from Microsoft.

## User Interface

New field on page VAT Posting Setup, Sales Line & Service Line.
Sales and Service Statistics.
New columns from VAT Entry are printed on Sales invoice and Sales Credit Memo.