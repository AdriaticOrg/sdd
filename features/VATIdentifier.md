# VAT Identifier

VAT Identifier table and field in VAT Entries functionality enables to use added table for VAT identifiers when setting up new combination of VAT posting setup from predefined VAT identifiers and transferring of VAT identifier from VAT posting group combination to VAT Entries at the time of posting document.

> Range: 13.062.591..13.062.600

## Scope

VAT Identifier is used for reporting filtering. To simplify filtering this feature copies VAT Identifier from VAT Porting Setup to VAT Entires.

## Architectural Design 

Create new table `VAT Identifier` and link it with `VAT Posting Setup`. This will prevent user from using wrong value. You will not be able to link directly. Workaround is to override validation and lookup. Add `VAT Identifier` field to `VAT Entry` table and make sure it's updated while posting VAT. 

## Data Design

### New table VAT Identifier

Name|Type
----|----
Code|Code[20]
Description|Text[50]

### Add new field to VAT Entry

Name|Type
----|----
VAT Identifier|Code[20]

## Data Flow

Process Name|Scope|Proposed Event
------------|-----|--------------
VAT Posting Setup Validation|Test if your value fits VAT Identifier table content|`"VAT Posting Setup".OnValidateVATIdentifier`
VAT Posting Setup Lookup|Enable lookup from VAT Posting Setup|`"VAT Posting Setup".OnLookupVATIdentifier`
Copy value to VAT Entry|When posting VAT also copy calculated value to VAT Entry|`"VAT Entry".OnAfterCopyFromGenJnlLine`

## User Interface

User must be able to select VAT Identifier from list. Create new list `"VAT Identifiers"`.