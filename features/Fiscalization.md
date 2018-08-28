# Fiscalization

> Range: 13.062.601..13.062.630

> Country: HR, SI

## Current object related to this feature

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Table|17|G/L Entry
2.|Table|21|Cust. Ledger Entry
3.|Table|36|Sales Header
4.|Table|81|Gen. Journal Line
5.|Table|91|User Setup
6.|Table|112|Sales Invoice Header
7.|Table|114|Sales Cr. Memo Header
8.|Table|254|Vat Entry
9.|Table|289|Payment Method
10.|Table|382|CV Ledger Entry Buffer
11.|Table|5900|Service Header
12.|Table|5992|Service Invoice Header
13.|Table|5994|Service Cr.Memo Header
14.|Codeunit|80|Sales-Post
15.|Codeunit|226|CustEntry-Apply Posted Entries
16.|Codeunit|1305|Sales-Quote to Invoice
17.|Codeunit|5923|Service-Quote to Order
18.|Codeunit|5988|Serv-Documents Mgt.

## Feature requirement

Feature Fiscalization enables direct real-time communication between Navision and Tax authority
Centralized Information System (aka CIS). Only Sales invoices or Credit Memos with selected payment methods must be reported after posting. After document posting this functionality creates xml data and sends this data via Web Service to CIS. CIS responds with unique ID or raises an error. If Unique ID is received it is saved in database. This ID appears on printed Sales invoice or Sales credit Memo.

Fiscalization locations must also be reported. Fiscalization location is real location with address, working hours and other attributes. Sales document must be issued from reported fiscalization locations.

## New Required Objects

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Table Extension|New Object|Tab17-Extxxxx.GLEntry-ADL
2.|Table Extension|New Object|Tab21-Extxxxxx.CustLedgerEntry-ADL
3.|Table Extension|New Object|Tab36-Extxxxxx.SalesHeader-ADL
4.|Table Extension|New Object|Tab81-Extxxxxx.GenJournalLine-ADL
5.|Table Extension|New Object|Tab91-Extxxxxx.UserSetup-ADL
6.|Table Extension|New Object|Tab112-Extxxxxx.SalesInvoiceHeader-ADL
7.|Table Extension|New Object|Tab114-Extxxxxx.SalesCrMemoHeader-ADL
8.|Table Extension|New Object|Tab254-Extxxxxx.VATEntry-ADL
9.|Table Extension|New Object|Tab289-Extxxxxx.PaymentMethod-ADL
10.|Table Extension|New Object|Tab382-Extxxxxx.CVLedgerEntryBuffer-ADL
11.|Table Extension|New Object|Tab5900-Extxxxxx.ServiceHeader-ADL
12.|Table Extension|New Object|Tab5992-Extxxxxx.ServiceInvoiceHeader-ADL
13.|Table Extension|New Object|Tab5994-Extxxxxx.ServiceCrMemoHeader-ADL
14.|Table|New Object|Tabxxxxx.FiscalizationSetup-ADL
15.|Table|New Object|Tabxxxxx.FiscalizationTerminal-ADL
16.|Table|New Object|Tabxxxxx.FiscalizationLocation-ADL
17.|Table|New Object|Tabxxxxx.FiscalizationLocationMapping-ADL
18.|Table|New Object|Tabxxxxx.FiscalizationPaymentMethod-ADL
19.|Page Extension|New Object|Pag17-Extxxxxx.GLEntry-ADL
20.|Page Extension|New Object|Pag21-Extxxxxx.CustLedgerEntry-ADL
21.|Page Extension|New Object|Pag36-Extxxxxx.SalesHeader-ADL
22.|Page Extension|New Object|Pag91-Extxxxxx.UserSetup-ADL
23.|Page Extension|New Object|Pag112-Extxxxxx.SalesInvoiceHeader-ADL
24.|Page Extension|New Object|Pag114-Extxxxxx.SalesCrMemoHeader-ADL
25.|Page Extension|New Object|Pag254-Extxxxxx.VATEntry-ADL
26.|Page Extension|New Object|Pag289-Extxxxxx.PaymentMethod-ADL
27.|Page Extension|New Object|Pag382-Extxxxxx.CVLedgerEntryBuffer-ADL
28.|Page Extension|New Object|Pag5900-Extxxxxx.ServiceHeader-ADL
29.|Page Extension|New Object|Pag5992-Extxxxxx.ServiceInvoiceHeader-ADL
30.|Page Extension|New Object|Pag5994-Extxxxxx.ServiceCrMemoHeader-ADL
31.|Page|New Object|Pagxxxxx.FiscalizationSetup-ADL
32.|Page|New Object|Pagxxxxx.FiscalizationTerminal-ADL
33.|Page|New Object|Pagxxxxx.FiscalizationLocation-ADL
34.|Page|New Object|Pagxxxxx.FiscalizationLocationMapping-ADL
35.|Page|New Object|Pagxxxxx.FiscalizationPaymentMethod-ADL
36.|Codeunit|New Object|Codxxxxx.ALxxxxx (Fiscalization Management)


1. Table Extension 17
    - 1 new field
      - Full Fisc. Doc. No.

2. Table Extension 21
    - 1 new fields
      - Full Fisc. Doc. No

3. Table Extension 36
    - 6 new fields 
      - Fisc. Subject
      - Fisc. No. Series
      - Fisc. Terminal
      - Fisc. Location Code
      - Fisc. Doc. No.
      - Full Fisc. Doc. No.

4. Table Extension 81
    - 1 new field
      - Full Fisc. Doc. No

5. Table Extension 91
    - 1 new field
      - Operator Tax Number

6. Table Extension 112
    - 8 new fields
      - Fisc. Subject
      - Fisc. No. Series
      - Fisc. Terminal
      - Fisc. Location Code
      - Fisc. Doc. No.
      - Fisc. Date
      - Fisc. Time
      - Full Fisc. Doc. No.

7. Table Extension 114
    - 8 new fields
      - Fisc. Subject
      - Fisc. No. Series
      - Fisc. Terminal
      - Fisc. Location Code
      - Fisc. Doc. No.
      - Fisc. Date
      - Fisc. Time
      - Full Fisc. Doc. No.

8. Table Extension 254
    - 1 new field
      - Full Fisc. Doc. No

9. Table Extension 289
    - 1 new field
      - Fisc. Payment Method

10. Table Extension 382
    - 1 new field
      - Full Fisc. Doc. No.

11. Table Extension 5900
    - 6 new fields 
      - Fisc. Subject
      - Fisc. No. Series
      - Fisc. Terminal
      - Fisc. Location Code
      - Fisc. Doc. No.
      - Full Fisc. Doc. No.

12. Table Extension 5992
    - 8 new fields
      - Fisc. Subject
      - Fisc. No. Series
      - Fisc. Terminal
      - Fisc. Location Code
      - Fisc. Doc. No.
      - Fisc. Date
      - Fisc. Time
      - Full Fisc. Doc. No.

13. Table Extension 5994
    - 8 new fields
      - Fisc. Subject
      - Fisc. No. Series
      - Fisc. Terminal
      - Fisc. Location Code
      - Fisc. Doc. No.
      - Fisc. Date
      - Fisc. Time
      - Full Fisc. Doc. No.

14. Table Fiscalization Setup
    - 5 fields
      - Active
      - Start Date
      - End Date
      - Default Fiscalization Location
      - Default Fiscalization Terminal

15. Table Fiscalization Terminal
    - 6 fields
      - Fisc. Terminal Code
      - Name
      - Fisc. No. Series
      - User ID
      - Creation Date
      - Creation Time

16. Table Fiscalization Location
    - 16 fields
      - Fisc. Location Code
      - Fisc. Street
      - Fisc. House Number
      - Fisc. House Number Appendix
      - Fisc. Settlement
      - Fisc. City/Municipality
      - Fisc. Post Code
      - Fisc. Location Description
      - Working Hours
      - Date of Application
      - Fisc. No. Series
      - Fisc. Active
      - Creation Date
      - Creation Time
      - User ID
      - Ending Date

17. Table Fiscalization Location Mapping
    - 2 fields
      - Location Code
      - Fisc. Location Code

18. Table Fiscalization Payment Method
    - 2 fields
      - Code
      - Description
      - Official Code
      - Subject to Fiscalization
      - Multiple Payment Methods


## Current object related to this feature

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Table|112|Sales Invoice Header
2.|Table|114|Sales Cr. Memo Header

## Feature requirement

Time stamp in G/L Register enables additional information about start and end time of posting in G/L Register, posting time in VAT Entry and posting time in Posted Sales Invoice and Sales Credit Memo Header.

Due to Fiscalization Feature Creation Time Stamp was added to sales invoice and credit memo. Tax authorities must identify when request was send. For measuring purposes two fields was added to G/L Register table: Creation Start Time and Creation End Time. Fields are automatically filled when document is posted.

## New Required Objects

No.|Type|Object ID|Name
--:|----|-----------:|--------
1.|Table Extension|New Object|Tab112-Extxxxxx.SalesInvoiceHeader-ADL
2.|Table Extension|New Object|Tab114-Extxxxxx.SalesCrMemoHeader-ADL
3.|Codeunit|New Object|Codxxxxx.ALxxxxx

1. Table Extension 112
    - 1 new field 
      - Posting TimeStamp

2. Table Extension 114
    - 1 new field 
      - Posting TimeStamp

3. Codeunit will have functions that will be triggered from Codeunit 80 after creating(Inserting) Invoice or CrMemoHeader. This codeunit will fill new field in Table Extension 112 and 114.