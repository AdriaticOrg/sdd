# Unpaid Receivables

According to Croatian Accounting Law every company need to report overdue and unpaid receivables
to Tax authorities. For this purpose, the government has made form that is called OPZ-STAT-1 (Overdue and uncollected receivables). The report must contain data on issued invoices which were not collected/paid within the legal or agreed period.

About the overdue and unpaid receivables obligors should prepare statistical reports with the balance of the current year on the day of the payment in whole or in overall write-off. The form is submitted for due but unpaid receivables as of the last day of the expiry of each quarter.

## Current objects related to this feature

No.|Type|Object ID|Name
--:|----|-----------:|--------
1. |Table |81  |Gen. Journal Line
2. |Table |254  |VAT Entry
3. |Codeunit |12  |Gen. Jnl.-Post Line
4. |Page|39|General Journal

## New required objects

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Table Extension|New Object|Tab81-Extxxxxx.GenJournalLine-ADL
2.|Page Extension|New Object|Pag39-Extxxxxx.GeneralJournal-ADL
3.|Codeunit|New Object|Codxxxxx.ALxxxxx
4.|Report|New Object|RepxxxxOverdueAndUncollectedRec-ADL

1. Table Extension 81
    - 2 new fields 
      - Original Document Amount (LCY)
      - Original VAT Amount (LCY)

2. Page Extension 39
    - 2 new fields 
      - Original Document Amount (LCY)
      - Original VAT Amount (LCY)

3. Codeunit will have functions that will be triggered from Codeunit 12 after posting. This codeunit will create and wright data in table 17,21,254.

4. Report will contain data on issued invoices which were not collected/paid within the legal or agreed period.

## Data Flow before changes

<img src=".\img\DataFlow_UnapidReceivables.png" width="500">

Standard posting of General Journal Line goes trought Codeunit 12 and creates several transaction records in different table among them are: 17,21,254.

## Data Flow after changes

<img src=".\img\DataFlow_UnapidReceivables_New.png" width="500">

For unpaid receivables user will enter additional data (Original Document Amount (LCY) and Original VAT Amount (LCY)) in General Journal Line. During posting process it will post additional entries into tables: 17,21,254.

>Note: This fields will be used only for Opening entries.