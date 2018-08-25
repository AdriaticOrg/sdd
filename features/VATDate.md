# VAT Date

VAT Date functionality enables posting of VAT on a different date as posting date. VAT Date is transferred to VAT and General ledger entries and used in corresponding reports and functionalities (VAT calculation, VAT Statement etc.). VAT Date is added to General Journal, Sales, Purchase and Service documents.

## Scope

User must be able to enter different VAT date then usual Posting date to indicate VAT will be reported in different period. 

## Architectural Design

Field is part of all Sales, Purchase and Service documents and finally to General Journal Line. When VAT date is different then Posting Date Postponed VAT feature is used to produce needed transactions. Finally VAT Date must be printable also on posted documents. 

## Data Design

Add VAT Date field to all Sales, Purchase and Service documents and Journal lines.
Table Name|Type
-|-
Sales Header|Document
Purchase Header|Document
Service Header|Document
Gen. Journal Line|Journal
Sales Invoice Header|Posted Document
Sales Cr.Memo Header|Posted Document
Purch. Inv. Header|Posted Document
Purch. Cr. Memo Hdr.|Posted Document
Service Invoice Header|Posted Document
Service Cr.Memo Header|Posted Document

## Data Flow

Process Name|Scope|Proposed Event
-|-|-
Document Validation|When entering Posting Date copy VAT Date if VAT date is empty|Document - Posting Date - OnValidate
Post - Create Journal|Copy VAT Date from Sales / Purchase / Service Document to General Journal Line|
Post - Create Transactions| When Posting Date and VAT Date is different it should produce additional VAT Entry. 
Post - Create Posted Document| Copy VAT date from Sales 

## User Interface

VAT Date should be available on Documents for editing, General Journal for editing, Posting documents for viewing.  