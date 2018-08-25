# FAS Reporting

According to Bank of Slovenian rules, business entities, who are requested to submit finance account statistics data, should report data on the state of financial assets and liabilities in financial accounts and on transaction changes in value of financial assets and liabilities.

The data for financial accounts statistics must be submitted by all institutional units which, according to the standard classification of institutional sectors according to the regulation, are classified into sectors 11, 12 and 13 and are determined by the decision on reporting or the criteria for assessing the reporting obligations by the Bank of Slovenia:

-for sector 11 or non-financial corporations, the balance sheet total (asset value) at the end of the calendar year prior to the reporting period, EUR 2 million or more,

-for sector 12 or financial corporations, the balance sheet total (asset value) at the end of the calendar year, before the period for which data are reported, EUR 1 million or more,

-for sector 13 or institutional units of central and local government, the balance sheet total (asset value) at the end of the calendar year, before the reporting period, is EUR 8 million or more.

Institutional units established during the year assess the reporting obligation by assessing the balance sheet at the end of the quarter for which data are reported.

## Scope

User must be able to add setup the necessary data for FAS reporting and print the report which also has the option to export data to xml file. Setup includes filling two additional fields: FAS Sector Code and FAS Instrument Code on relevant master tables.

## Architectural Design

FAS Sector Code and FAS Instrument Code are added to relevant master tables like Customer, Vendor etc, on general journal and general ledger entries. During any financial posting which results in a general ledger, both fields are populated.

## Data Desgin

Fields FAS Sector Code and/or Instrument Code are added to following tables

ID|Name
--:|----
9|Country/Region
15|G/L Account
17|G/L Entry
81|Gen. Journal Line
18|Customer
23|Vendor
270|Bank Account
5050|Contact
92|Customer Posting Group
93|Vendor Posting Group
277|Bank Account Posting Group

New objects are

Type|Name
--|----|
Table Extension|CountryRegion-adl
Table Extension|GLAccount-adl
Table Extension|GLEntry-adl
Table Extension|GenJnlLine-adl
Table Extension|Customer-adl
Table Extension|Vendor-adl
Table Extension|BankAccount-adl
Table Extension|Contact-adl
Table Extension|CustPstGroup-adl
Table Extension|VendPstGroup-adl
Table Extension|BankAccPstGroup-adl
<br>|<br>
Page Extension|Countries-adl
Page Extension|GLAccountCard-adl
Page Extension|GLEntries-adl
Page Extension|GenJnlLine-adl
Page Extension|CustomerCard-adl
Page Extension|VendorCard-adl
Page Extension|BankAccountCard-adl
Page Extension|ContactCard-adl
Page Extension|CustPstGroups-adl
Page Extension|VendPstGroups-adl
Page Extension|BankAccPstGroups-adl
<br>|<br>
Table|FAS Sector
Table|FAS Instrument
Table|FAS Setup
Table|FAS Header
Table|FAS Line
<br>|<br>
Page|FAS Report
Page|FAS Report Subform
<br>|<br>
Report|FAS Suggest Lines
Report|FAS Report

## Data Flow

Process Name|Scope|Proposed Event
--|--|--
Journal validation|When entering Account No. copy Finance and/or Sector Code from relevant tables i.e Customer, Vendor, G/L Account, Bank Account|General Journal - Account No. - OnValidate
Gen. Journal Line posting|Transfer Finance and Sector Code from Gen. Journal Line to G/L Entry. If data not available in Gen. Journal Line, try to get them from master tables (Customer, Vendor, Bank Account)|
Report preparing|Open new Reporting document for the period in question, run the suggest lines process to populate Reporting document lines. Run the FAS Report to get the hard copy and/or xml file saved to disk.|

## User Interface

Finance and Sector Code should be visible on relevant page extensions for viewing and/or editing.

>Note: file may be altered in near future.