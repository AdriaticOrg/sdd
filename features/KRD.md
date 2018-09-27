# KRD Report

KRD Report (International Payables and Receivables Report) enables reporting of KRD report, which is used to report short term receivables and payables with foreign partners to Bank of Slovenia (BSI) on monthly basis grouped by currency, country and capital ties. Report is submitted electronically.

> Range: 13.062.661..13.062.680

> Country: SI

## Scope

User must be able to setup the necessary data for KRD reporting and print the report which also has the option to export data to xml file. In general, besides KRD Setup, setup process includes filling some additional fields on master and subsidiary tables (Customer, Vendor, Customer Posting Group, Vendor Posting Group). Prior to this action, relevant KRD Code record should be inserted.

## Architectural Design

Customers and Vendors have two attribute fields added:
> KRD Non-Resident Sector Code-Adl: specifies the financial sector of business entity.

> KRD Affiliation Type-Adl: defines the relation between business entities

On Customer Posting Groups and Vendor Posting Groups level we define other attributes:
> KRD Claim/Liability: defines the financial direction of the trade transaction.

> KRD Instrument Type-Adl: specifies the type of financial transaction.

> KRD Maturity-Adl: means time length or span of financial transaction. 

All these data is gathered during posting sales or purchase transactions and ends in resulting Vendor and Customer Ledger Entry records, which are source where the KRD report data will be taken from.

## Data Design

The relevant KRD fields are added to the following existig tables:

ID|Name
--:|----
18|Customer
23|Vendor
21|Cust. Ledger Entry
25|Vendor Ledger Entry
92|Customer Posting Group
93|Vendor Posting Group

New objects are:

Type|Name
--|----|
Table Extension|Customer-Adl
Table Extension|Vendor-Adl
Table Extension|Cust. Ledger Entry-Adl
Table Extension|Vendor Ledger Entry-Adl
<br>|<br>
Page Extension|Customer Card-Adl
Page Extension|Vendor Card-Adl
Page Extension|Customer Ledger Entries-Adl
Page Extension|Vendor Ledger Entries-Adl
<br>|<br>
Table|KRD Setup-Adl
Table|KRD Code-Adl
Table|KRD Sector-Adl
Table|KRD Report Header-Adl
Table|KRD Report Line-Adl
<br>|<br>
Page|KRD Setup-Adl
Page|KRD Codes-Adl
Page|KRD Sectors-Adl
Page|KRD Reports-Adl
Page|KRD Report-Adl
Page|KRD Report Subform-Adl
<br>|<br>
Report|Suggest KRD Lines-Adl
Report|Export KRD-Adl

## Data Flow

Process Name|Scope
--|--
Sales/Purchase document posting|When data is transfered to Customer/Vendor Ledger Entry, we transfer new added fields too, data is taken from Customer/Vendor and from Customer/Vendor Posting Group respectively.
Report preparing|Open new Reporting document for the period in question, run the suggest lines process to populate Reporting document lines. Manually adjust lines if needed. Run the Export KRD activity to get the hard copy and/or xml file saved to disk.|

## User Interface

New KRD related filedls should be visible on relevant page extensions for viewing and/or editing.

>Note: this file may be subject of change in near future if need arises.