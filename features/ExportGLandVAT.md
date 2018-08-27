# Export GL and VAT

## Feature requirement

Export GL and VAT Ledgers on Tax Authorities demand exporting VAT books and G/L ledgers electronically in fix text format prescribed by Tax authorities.

## Scope

This feature manages exporting data in fixed text format. 3 reports are covered:

1. Chart of Accounts
2. Input VAT Book
3. Output VAT Book

## Architectural Design 

Create new object CODEUNIT Text Writer-adl that covers exporting capabilities:

``` PAS
PROCEDURE Open(FieldDelimiter: text; RecordDelimiter: text);
PROCEDURE Field(Value: variant);
PROCEDURE FixedField(Value: variant; Length: integer);
PROCEDURE NewLine;
PROCEDURE Close;
PROCEDURE Download(LocalFileName: text);
``` 

For each export prepare Report object. Use request page for filtering and data sources for looping through records. Use Text Writer codeunit to export fields as requested in Appendix.

> Note: User must be able to start exports from expected point (See User Interface). Therefore new VAT Statement books needs to be set up.

VAT Statement Template has VAT Statement Report ID filed which should start right report.
Use VAT Statement Column from [VAT Books feature](VATBooks.md) that identifies layout.

## Data Design

See appendix for detailed export requirements.

## Data Flow

Data is filtered in report and exported during report (Process Only) flow. 

## User Interface

User starts export from place related to data that is exporting:

1. Chart of Accounts from Chart of Accounts clicks export.
2. Input VAT Book from VAT Statement, selects INPUT VAT statement and clicks export, fills requested filters.
3. Output VAT Book from VAT Statement, selects OUTPUT VAT statement and clicks export, fills requested filters.


## Appendix

No.|Appendix Document
---|-----------------
1. |[Char of Account](ExportGLandVAT/ChartOfAccount.md)
2. |[Input VAT Books](ExportGLandVAT/InputVATBook.md)
3. |[Output VAT Books](ExportGLandVAT/OutputVATBook.md)

