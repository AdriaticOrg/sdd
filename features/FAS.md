# FAS Report

According to Bank of Slovenian rules, business entities, who are requested to submit finance account statistics data, should report data on the state of financial assets and liabilities in financial accounts and on transaction changes in value of financial assets and liabilities.

The data for financial accounts statistics must be submitted by all institutional units which, according to the standard classification of institutional sectors according to the regulation, are classified into sectors 11, 12 and 13 and are determined by the decision on reporting or the criteria for assessing the reporting obligations by the Bank of Slovenia:

-for sector 11 or non-financial corporations, the balance sheet total (asset value) at the end of the calendar year prior to the reporting period, EUR 2 million or more,

-for sector 12 or financial corporations, the balance sheet total (asset value) at the end of the calendar year, before the period for which data are reported, EUR 1 million or more,

-for sector 13 or institutional units of central and local government, the balance sheet total (asset value) at the end of the calendar year, before the reporting period, is EUR 8 million or more.

Institutional units established during the year assess the reporting obligation by assessing the balance sheet at the end of the quarter for which data are reported.

> Range: 13.062.641..13.062.660

> Country: SI

## Scope

User must be able to setup the necessary data for FAS reporting and print the report which also has the option to export data to xml file. In general, besides FAS Setup, setup process includes filling two additional fields: FAS Sector Code-Adl and FAS Instrument Code-Adl on relevant master tables. Prior to this action, FAS Sector and FAS Instrument records should be inserted.

## Architectural Design

FAS Sector Code-Adl and FAS Instrument Code-Adl are added to relevant master tables like Customer, Vendor etc, on General Journal and General Ledger Entries. During any financial posting which results in a General Ledger Entry, both fields are populated if available. On G/L Account we have a few more additional fields:
> FAS Account-Adl: indicates we want to enable FAS.

> FAS Type-Adl: indicates direction of inclusion on FAS report (Assets or Liabilities).

> FAS Instrument Posting-Adl, FAS Sector Posting-Adl: is used to apply restrictions on posting.


## Data Design

Fields FAS Account-Adl, FAS Type-Adl, FAS Instrument Posting-Adl, FAS Sector Posting-Adl are added to table 15 G/L Account.

Fields FAS Sector Code and/or Instrument Code are added to following tables

ID|Name
--:|----
15|G/L Account
17|G/L Entry
81|Gen. Journal Line
18|Customer
23|Vendor
270|Bank Account

New objects are:

Type|Name
--|----|
Table Extension|Country/Region-Adl
Table Extension|G/L Account-adl
Table Extension|Gen. Journal Line-Adl
Table Extension|Customer-Adl
Table Extension|Vendor-Adl
Table Extension|Bank Account-Adl
<br>|<br>
Page Extension|Countries/Regions-Adl
Page Extension|G/L Account Card-Adl
Page Extension|General Ledger Entries-Adl
Page Extension|General Journal-Adl
Page Extension|Customer Card-Adl
Page Extension|Vendor Card-Adl
Page Extension|Bank Account Card-Adl
<br>|<br>
Table|FAS Setup-Adl
Table|FAS Sector-Adl
Table|FAS Instrument-Adl
Table|FAS Report Header-Adl
Table|FAS Report Line-Adl
<br>|<br>
Page|FAS Reports-Adl
Page|FAS Report-Adl
Page|FAS Report Subform-Adl
<br>|<br>
Report|Suggest FAS Lines-Adl
Report|Export FAS-Adl

## Data Flow

Process Name|Scope
--|--
Sales/Purchase document posting|When data is transfered to Gen. Journal Line, we transfer new added fields too.
Journal validation|When entering Account No. and Bal. Account No. in General Journal Line, copy FAS Instrument Code-Adl and/or FAS Sector Code-Adl from relevant tables i.e Customer, Vendor, G/L Account, Bank Account. 
Gen. Journal Line posting|Transfer FAS Sector Code-Adl and FAS Instrument-Adl from Gen. Journal Line to G/L Entry. If data not available in Gen. Journal Line, try to get them from master tables (Customer, Vendor, Bank Account)|
Report preparing|Open new Reporting document for the period in question, run the suggest lines process to populate Reporting document lines. Manually adjust lines if needed. Run the Export FAS activity to get the hard copy and/or xml file saved to disk.|

## User Interface

New FAS related filedls should be visible on relevant page extensions for viewing and/or editing.

>Note: this file may be subject of change in near future if need arises.