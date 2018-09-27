# PDO Feature
PDO Feature is meant to cover business needs when a taxable person who supplies goods and services for which the recipient is VAT payer based on 76.a article in Slovenian law ZDDV-1.
Taxable person must draw up a report on these deliveries for the calendar month in which the relevant parties have carried out of supply, and/or for which it must report the corrected information about the supplies concerned from previous periods.

> Range: 13.062.621..13.062.640

> Country: SI

## Scope

User must be able to setup the necessary data for PDO reporting and print the report which also has the option to export data to xml file. In general, besides PDO Setup, setup process includes filling an additional field VAT % (informative)-Adl in VAT Posting Setup records, where specific records indicate selling goods or services according to 76. article of ZDDV-1 law.

## Architectural Design

VAT % (informative)-Adl is added to VAT Posting Setup table. No additional business logic to transfer values to entry tables is implemented. Process of gathering data for PDO report is based on data from VAT Entry records, where process will take into consideration also values from VAT Posting Setup. 

## Data Design

Field VAT % (informative)-Adl is added to 325 VAT Posting Setup table.

New objects are:

Type|Name
--|----|
Table Extension|VAT Posting Setup-Adl
<br>|<br>
Page Extension|"VAT Posting Setup-Adl"
<br>|<br>
Table|PDO Setup-Adl
Table|PDO Report Header-Adl
Table|PDO Report Line-Adl
<br>|<br>
Page|PDO Setup-Adl
Page|PDO Reports-Adl
Page|PDO Report-Adl
Page|PDO Report Subform-Adl
<br>|<br>
Report|Suggest PDO Lines-Adl
Report|Export PDO-Adl

## Data Flow

Process Name|Scope
--|--
Report preparing|Open new Reporting document for the period in question. Run the suggest lines process to populate Reporting document lines. Manually adjust lines if needed. Run the Export PDO activity to get the hard copy and/or xml file saved to disk.|

## User Interface

New PDO related filedls should be visible on relevant page extensions for viewing and/or editing.

>Note: this file may be subject of change in near future if need arises.
