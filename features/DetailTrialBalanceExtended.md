# Detail Trial Balance Extended 

## Current object related to this feature

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Table|91|User Setup
2.|Table|98|General Ledger Setup 
3.|Page|118|General Ledger Setup
4.|Page|119|User Setup

## Feature requirement

According to Croatian Accounting Law from 01.01.2016 every transaction that is posted in G/L Register needs to have Posting Responsible person and Posting Approver. Due to this change new report for Detail trial balance need to be created and one for every transaction users needs to print posting schema.

## New Required Objects

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Table Extension|New Object|Tab91-Extxxxxx.User Setup-ADL
2.|Table Extension|New Object|Tab98-Extxxxxx.GeneralLedgerSetup-ADL
3.|Page Extension|New Object|Page118-Extxxxxx.GeneralLedgerSetup-ADL
4.|Page Extension|New Object|Page119-Extxxxxx.UserSetup-ADL
5.|Report|New Object|RepxxxxDetailTrialBalance-ADL

1. Table Extension 91
    - 2 new fields 
      - Posting Responsible Person
      - Posting Approver

2. Table Extension 98
    - 2 new fields 
      - Global Posting Resp. Person
      - Global Posting Approver

3. Page Extension 118
    - 2 new fields 
      - Posting Responsible Person
      - Posting Approver

4. Page Extension 119
    - 2 new fields 
      - Global Posting Resp. Person
      - Global Posting Approver

5. Report will be similar to report Detail Trial Balance (Report 4) and will have additional fields (Posting Responsible Person, Posting Approver). Fields will be populated from Field Approver ID from User ID which posted the entry. In case Approver ID is empty on User Setup Table fields will be populated from New fields on General Ledger Setup. Printing for one transaction must be possible.
