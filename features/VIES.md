# VIES Feature

VIES aka recapitulative report in Slovenia is a report, a taxable person identified for VAT purposes in Slovenia shall show the supplies of goods and services that are delivered to persons identified for VAT in the other EU Member States during the reporting period, that is, the calendar month.

Vies in Slovenia is about reporting sales, while in Crotia we have two subtypes of it. Subtype ZP conforms with slovenian one, while subtype PDV-S contains purchases from other EU states.

VIES feature functionality enables preparation of VIES report according to Adriatic legislation by using of improved standard VIES functionality.

> Range: 13.062.601..13.062.620

> Country: SI, HR

## Scope

User must be able to setup the necessary data for VIES reporting and print the report which also has the option to export data to xml file. In general, besides VIES Setup, setup process includes filling an additional field VIES Goods-Adl in VAT Posting Setup records, where specific records indicates selling/purchasing goods to/from EU states.

## Architectural Design

VIES Goods-Adl is added to VAT Posting Setup table. No additional business logic to transfer values to entry tables is implemented. Process of gathering data for VIES report is based on data from VAT Entry records, where process will take into consideration also values from VAT Posting Setup. 

## Data Design

Field VIES Goods-Adl is added to 325 VAT Posting Setup table.

New objects are:

Type|Name
--|----|
Table Extension|VAT Posting Setup-Adl
<br>|<br>
Page Extension|"VAT Posting Setup-Adl"
Page Extension|VAT Entries-Adl
<br>|<br>
Table|VIES Setup-Adl
Table|VIES Report Header-Adl
Table|VIES Report Line-Adl
<br>|<br>
Page|VIES Setup-Adl
Page|VIES Reports-Adl
Page|VIES Report-Adl
Page|VIES Report Subform-Adl
<br>|<br>
Report|Suggest VIES Lines-Adl
Report|Export VIES-Adl

## Data Flow

Process Name|Scope
--|--
Report preparing|Open new Reporting document for the period in question. Select proper VIES Country and VIES Type. Run the suggest lines process to populate Reporting document lines. Manually adjust lines if needed. Run the Export VIES activity to get the hard copy and/or xml file saved to disk.|

## User Interface

New VIES related filedls should be visible on relevant page extensions for viewing and/or editing.

>Note: this file may be subject of change in near future if need arises.
