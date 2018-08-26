# Software Design Document

A software design description (a.k.a. software design document or SDD), also Software Design Specification is a written description of a software product, that a software designer writes in order to give a software development team overall guidance to the architecture of the software project. An SDD usually accompanies an architecture diagram with pointers to detailed feature specifications of smaller pieces of the design. Practically, the description is required to coordinate a large team under a single vision, needs to be a stable reference, and outline all parts of the software and how they will work. [More on wiki.](https://en.wikipedia.org/wiki/Software_design_description)

## Feature List

Supported features:

Module|Feature Name|Country Specific
-----|------------|----------------
VAT Posting|[VAT Date](features/VATDate.md)|All
VAT Posting|[VAT Identifier](features/VATIdentifier.md)|All
VAT Posting|[Postponed VAT](features/PostponedVAT.md)|All
VAT Posting|[Full VAT Posting](features/FullVATPosting.md)|All
VAT Posting|[Reverse Charge Posting](features/ReverseChargePosting.md)|All
VAT Posting|[Informative VAT](features/InformativeVAT.md)|SI
General Ledger|[Red reversal Posting](features/RedReversalPosting.md)|All
General Ledger|[Forced Debit / Credit Posting](features/ForcedDebitCreditPosting.md)|All
Sales & Purchase|[Internal Correction](features/InternalCorrection.md)|All
Sales & Purchase|[Return Orders](features/ReturnOrders.md)|All
Sales & Purchase|[Sales Documents](features/SalesDocuments.md)|All
Sales & Purchase|[Fiscalization](features/Fiscalization.md)|HR,SI
Reporting|[VAT Books](features/VATBooks.md)|All
Reporting|[Export G/L and VAT](features/ExportGLandVAT.md)|SI
Reporting|[VIES Feature](features/VIES.md)|SI
Reporting|[Delivery Declaration](features/DeliveryDeclaration.md)|SI
Reporting|[FAS Report](features/FAS.md)|SI
Reporting|[KRD Report](features/KDR.md)|SI
Reporting|[BST Report](features/BST.md)|SI
Reporting|[Detail Trial Balance Extended](features/DetailTrialBalanceExtended.md)|HR
Reporting|[Unpaid Receivables](features/UnpaidReceivables.md)|HR

## How to write design?

Use [template](template/Template.md) as starting point. Follow instructions from template. Your goal is to write document that developer can read and understand. 
