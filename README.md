# Software Design Document

A software design description (a.k.a. software design document or SDD), also Software Design Specification is a written description of a software product, that a software designer writes in order to give a software development team overall guidance to the architecture of the software project. An SDD usually accompanies an architecture diagram with pointers to detailed feature specifications of smaller pieces of the design. Practically, the description is required to coordinate a large team under a single vision, needs to be a stable reference, and outline all parts of the software and how they will work. [More on wiki.](https://en.wikipedia.org/wiki/Software_design_description)

## Projects

Code|Name
----|----
VAT|[VAT Posting](https://github.com/AdriaticOrg/code/issues?q=is%3Aopen+is%3Aissue+project%3AAdriaticOrg%2Fcode%2F1)
GL|[General Ledger](https://github.com/AdriaticOrg/code/issues?q=is%3Aopen+is%3Aissue+project%3AAdriaticOrg%2Fcode%2F2)
SP|[Sales & Purchase](https://github.com/AdriaticOrg/code/issues?q=is%3Aopen+is%3Aissue+project%3AAdriaticOrg%2Fcode%2F3)
REP|[Reports](https://github.com/AdriaticOrg/code/issues?q=is%3Aopen+is%3Aissue+project%3AAdriaticOrg%2Fcode%2F4)


Supported features:

No.|Project|Feature Name|Country Specific
---|------|------------|----------------
1.|VAT Posting|[VAT Date](features/VATDate.md)|All
2.|VAT Posting|[VAT Identifier](features/VATIdentifier.md)|All
3.|VAT Posting|[Postponed VAT](features/PostponedVAT.md)|All
4.|VAT Posting|[Full VAT Posting](features/FullVATPosting.md)|All
5.|VAT Posting|[Reverse Charge Posting](features/ReverseChargePosting.md)|All
6.|VAT Posting|[Informative VAT](features/InformativeVAT.md)|SI
7.|General Ledger|[Red reversal Posting](features/RedReversalPosting.md)|All
8.|General Ledger|[Forced Debit / Credit Posting](features/ForcedDebitCreditPosting.md)|All
9.|Sales & Purchase|[Internal Correction](features/InternalCorrection.md)|All
10.|Sales & Purchase|[Return Orders](features/ReturnOrders.md)|All
11.|Sales & Purchase|[Sales Documents](features/SalesDocuments.md)|All
12.|Sales & Purchase|[Fiscalization](features/Fiscalization.md)|HR,SI
13.|Reporting|[VAT Books](features/VATBooks.md)|All
14.|Reporting|[Export G/L and VAT](features/ExportGLandVAT.md)|SI
15.|Reporting|[VIES Feature](features/VIES.md)|SI
16.|Reporting|[Delivery Declaration](features/DeliveryDeclaration.md)|SI
17.|Reporting|[FAS Report](features/FAS.md)|SI
18.|Reporting|[KRD Report](features/KDR.md)|SI
19.|Reporting|[BST Report](features/BST.md)|SI
20.|Reporting|[Detail Trial Balance Extended](features/DetailTrialBalanceExtended.md)|HR
21.|Reporting|[Unpaid Receivables](features/UnpaidReceivables.md)|HR

## How to write design?

Use [template](template/Template.md) as starting point. Follow instructions from template. Your goal is to write document that developer can read and understand. 
