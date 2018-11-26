# Return Orders

Return Order as new goods turnover functionality enables to include Sales Returns in VAT Purchase Book and Purchase Returns in VAT Sales Book in accordance to Value Added Tax Law.

> Range: 13.062.591..13.062.600

## Scope
User must be able to post Credit Memos and Return Orders with different VAT Bussines Posting Group, to get posted VAT entries with different VAT Identifier. User can change VAT Busines Posting Group when entering Code in new field Goods Return Type available on Sales and Purchase Credit Memos and also Return Orders. 

## Architectural Design 

Add new table "Goods Return Type" with following fields

Field|Type
-|-
Code|Code[10]
Description|Text250
VAT Bus. Posting Group|Code[10]

Add field Goods Return Type to following tables an pages:

Object Type|Object Name
-|-
Table|Sales Header
Table|Purchase Header
Table|Sales Cr. Memo Header
Table|Purch. Cr. Memo Header
Table|Return Shipment Header
Table|Return Receipt Header
Table|Service Header
Table|Service Cr.Memo Header
Page|Sales Credit Memo
Page|Purchase Credit Memo
Page|Posted Sales Credit Memo
Page|Posted Purchase Credit Memo
Page|Service Credit Memo
Page|Posted Service Credit Memos

On Validate of new field "Goods Return Type" validate "VAT Business Posting Group" with predefined value in table "Goods Return Type".

## Data Design

## Data Flow

Process Name|Scope|Proposed Event
-|-|-
Document Validation|When entering Goods Return Type copy VAT Business Posting Group from table Goods Return Type to VAT Business Posting Group|Document - Goods Return Type - OnValidate
Post - Create Posted Document| Goods Return Type date from Document 

## User Interface

Goods Return Type field should be available on documents for editing, and posting documents for viewing. Also new table Goods Return Type must be available to edit.
