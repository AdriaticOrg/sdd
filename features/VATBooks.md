# VAT Books

VAT Books functionality is used in addition to the periodic VAT statements that company submit in order to settle VAT. Tax Authority require to submit periodic reports of transactions including VAT. VAT books for Tax Authority and internal demand can be created through VAT books setup. Primary aim of this feature was to simplify and improve application setup and make it user friendly.

> Alias: KUF, KIF, POPDV, PPPDV, VAT Books

## Scope

Reports are typically based on VAT Entries records filtered by reporting period. First few columns are related to document that was posting (e.g. Customer / Vendor name, address, ...), and next of calculated values based on predefined filters. The output could be printed version or exported text or xml format.

## Architectural Design 

VAT Statement feature is already part of base code (W1), but it doesn't cover calculating columns. We will add tables to existing model for easier creation. Report will be added to test result with supporting 20 columns.  

## Data Design

Current tables related to available VAT Statement feature:

ID|Name|Description
--|----|-----------
255|VAT Statement Template|Template represents group of Statements where VAT Statement Report ID can be set up.
256|VAT Statement Line|Definition of statement rows.
257|VAT Statement Name|Is a header of statement with info of template.

This could be reused for VAT Books or VAT Statements with additional column setup.

### VAT Statement Column

Field Name|Type|Comment
----------|----|-------
VAT Statement Name|Code[10]|
Line No.|Integer|Use Auto split on pages.
Column No.|Integer|
Description|Text[50]|
Field Id|Integer|Related to Field Table filtered by VAT Entry
Field Name|Flow Field of Text[30]|Lookup to Field Table and Field Name based on Field Id
VAT Identifier Group|Code[20]|Linked to VAT Identifier Group
VAT Entry Filter|Text[250]|User interface should bring popup to make additional filter for VAT Entry.
Negative Sign|Boolean|

> Note: When Column No. is repeated it is expected that value will be added together in same column.

### VAT Identifier Group

VAT Identifier Group can be used to filter VAT Entries that matches content. So simple groups with list of VAT Identifiers.

Field Name|Type
----------|----
Code|Code[20]
Description|Text[80]
Group Type|Option[VAT Entries,Total]
Totaling|Text[250]
No. or Group Items|Integer (flow field as count of VAT Identifier Group Item)
XML Node Name|Text[100]

### VAT Identifier Group Item

Field Name|Type
----------|----
VAT Identifier Group Code|Code[20] link to VAT Identifier Group
Description|Text[80]

## Data Flow

### VAT Statement Calculation

Prepare separate Codeunit where cell from matrix will be calculated. 

```PAS
procedure CalculateCell(var VATEntry: Record "VAT Entry"; var Column: Record "VAT Statement Column") Result: Decimal;
// Repeat cell calculation for same column in use NegativeSign for reversing amount.

procedure CalculateSubCell(var VATEntry: Record "VAT Entry"; var Column: Record "VAT Statement Column") Result: Decimal;
// Use RecordRef on VAT Entry to simply assign Field and calculate sum based on filters.
// Filters must be obtained from entered VATEntry records, VAT Entry Filter field and VAT Identifier Group. 

procedure EvaluateExpression(VATBookGroup: Record "VAT Book Group"; ColumnNo: Integer; DateFilter: Text) Result: Decimal;
// Evaluate expression when group type is totaling. 

procedure GetVATIdentifierFilter(VATIdentifierGroupCode: Code[20]) Filter: Text;
// Create filter based on VAT Identifier Group.
```

### Report for VAT Statement

Create report and layout that will print out 20 columns of VAT Statement. 

## User Interface

User must be able to run reports from natural place (e.g. VAT Statement). Report could also start exporting data (see feature [Export G/L and VAT](features/ExportGLandVAT.md)).