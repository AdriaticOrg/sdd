# Output VAT Book

## File Format

Fixed .txt file in ASCII format, CP1250 code page.   
Field delimiter is semicolon ( ; ), record delimiter is CR LF.   
File name - IZPIS OBRAČUNANEGA DDV.TXT

## System Filters

Export VAT Entries where Amount or/and Base are not null. 

## Request Filters

- Posting Date - mandatory
- Document No.

## File Layout

No.|Position from|Position to|Length|Field Type|Field Name with description|Format/alignment|Export field name|NAV table|Field in NAV|VAT Identifier filter
---|-------------|-----------|------|----------|---------------------------|----------------|-----------------|---------|------------|---------------------
1|1|4|4|N|VAT periodPosting Date in format <Month,2><Month,2>|**Odb**|VAT Entry|Posting Date||
2|6|13|8|N|Posting date |format DDMMLLLL|**Dat knj**|VAT Entry|Posting Date||
3|15|44|30|AN|Document No. |the first 30 characters, left alignment|**Številka listine**|VAT Entry|Document No.||
4|46|53|8|N|Document date |format DDMMLLLL|**Dat lis**|VAT Entry|Document Date||
5|55|104|50|AN|Customer name and address |the first 50 characters, left alignment|**Kupec**|Posted document /Vendor /Customer|Bill-to Name, Bill-to Address, Bill-to City, Bill-to Country/Region Code||
6|106|125|20|AN|Customer VAT registration No. |the first 20 characters, left alignment|**IŠ za DDV**|VAT Entry|VAT Registration No.||
7|127|142|16|N|The value of sales of goods and services excluding VAT |right alignment, format -999999999999.99|**Vred brez DDV**|VAT Entry|Base|9, 10, 12, 14, 16, 18, 112, 114, 116, 118|
8|144|159|16|N|The value of sales of goods and services in Slovenia from reverse charge VAT | right alignment, format -999999999999.99|**Vred za samoobd**|VAT Entry|Base|35, 36|
9|161|176|16|N|The value of exempt sales in EU without no right for deduction |right alignment, format -999999999999.99|**OD brez pravice**|VAT Entry|Base|8, 82|
10|178|193|16|N|The value of exempt sales in EU |right alignment, format -999999999999.99|**Op dob Skupnost**|VAT Entry|Base|37|
11|195|210|16|N|The value of exempt sales 3-Party EU |right alignment, format -999999999999.99|**Op tristr dob**|VAT Entry|Base|39|
12|212|227|16|N|The value of remote sales of goods |right alignment, format -999999999999.99|**Prod dalj**|VAT Entry|Base|38, 608|
13|229|244|16|N|The value of sales of goods with installation |right alignment, format -999999999999.99|**Prod mont**|VAT Entry|Base|708|
14|246|261|16|N|Calculated VAT 22% |right alignment, format -999999999999.99|**OBR 22% DDV**|VAT Entry|VAT Amount|14, 18, 114, 118, 27|
15|263|278|16|N|Calculated VAT 9,5% |right alignment, format -999999999999.99|**OBR 9,5% DDV**|VAT Entry|VAT Amount|12, 16, 112, 116|
16|280|295|16|N|Calculated VAT 22% for sales for goods in EU |right alignment, format -999999999999.99|**OBR 22% DDV BL S**|VAT Entry|VAT Amount|312, 314, 4312, 4314, 318, 5314|
17|297|312|16|N|Calculated VAT 22% for sales for services in EU |right alignment, format -999999999999.99|**OBR 22 % DDV ST S**|VAT Entry|VAT Amount|16, 110, 5016, 4016, 4110, 28|
18|314|329|16|N|Calculated VAT 9,5% for sales for goods in EU | right alignment, format -999999999999.99|**OBR 9,5% DDV BL S**|VAT Entry|VAT Amount VAT|311, 313, 4311, 4313, 317|
19|331|346|16|N|Calculated VAT 9,5% for sales for services in EU |right alignment, format -999999999999.99|**OBR 9,5% DDV ST S**|VAT Entry|VAT Amount VAT|15, 109|
20|348|363|16|N|Calculated VAT 22% for sales f goods and services in Slovenia from reverse charge VAT |right alignment, format -999999999999.99|**OBR 22% DDV samo**|VAT Entry|VAT Amount|5141, 5041, 26, 4026, 108, 41, 141, 5043, 43, 5143, 143, 4041, 4141, 4043, 4143, 44, 5044, 4108|
21|365|380|16|N|Calculated VAT 9,5% for sales f goods and services in Slovenia from reverse charge VAT |right alignment, format -999999999999.99|**OBR 9,5% DDV samo**|VAT Entry|VAT Amount|5140, 5040, 25, 40, 140, 107, 5042, 42, 5142, 142, 4040, 4140, 4042, 4142|
22|382|397|16|N|Calculated VAT for sales f goods and services from export |right alignment, format -999999999999.99|**OBR DDV uvoz**|VAT Entry|VAT Amount|6023, 6013, 4623, 4613, 6053, 6063|
23|399|414|16|N|The value of sales with right for deduction outside SI |right alignment, format -999999999999.99|**Vred obdavčljiv**|VAT Entry|Base|808|
24|416|575|160|AN|Notes - not mandatory |left alignment|**Opombe**|VAT Entry|Posting Date