# VAT Identifier

VAT Identifier table and field in VAT Entries functionality enables to use added table for VAT identifiers when setting up new combination of VAT posting setup from predefined VAT identifiers and transferring of VAT identifier from VAT posting group combination to VAT Entries at the time of posting document.

## Scope

VAT Identifier is used for reporting filtering. To simplify filtering this feature copies VAT Identifier from VAT Porting Setup to VAT Entires.

## Architectural Design 

Create new table `VAT Identifier` and link it with `VAT Posting Setup`. This will prevent user from using wrong value. You will not be able to link directly. Workaround is to override validation and lookup. Add `VAT Identifier` field to `VAT Entry` table and make sure it's updated wile posting VAT. 

## Data Design

### VAT Identifier

Name|Type
----|----
Code|Code[20]
Description|Text[50]

## Data Flow

Process Name|Scope|Proposed Event
------------|-----|--------------
VAT Posting Setup Validation|Test if your value fits VAT Identifier table content|`"VAT Posting Setup".OnValidateVATIdentifier`
VAT Posting Setup Lookup|Enable lookup from VAT Posting Setup|`"VAT Posting Setup".OnLookupVATIdentifier`

## User Interface

User must be able to select VAT Identifier from list. Create new list `"VAT Identifires"`.