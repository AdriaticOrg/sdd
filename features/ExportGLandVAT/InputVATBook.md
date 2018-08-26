# Input VAT Book

## File Format

Fixed .txt file in ASCII format, CP1250 code page.   
Field delimiter is semicolon ( ; ), record delimiter is CR LF.   
File name - IZPIS ODBITKA DDV.TXT

Export VAT Entries where Amount or/and Base are not null. 

## Request Filters

- Posting Date - mandatory
- Document No.

## Layout

No.|Position from|Position to|Length|Field Type|Field Name with description|Format/alignment|Export field name|NAV table|Field in NAV|VAT Identifier filter|Type
---|-------------|-----------|------|----------|---------------------------|----------------|-----------------|---------|------------|---------------------|----
1|1|4|4|N|VAT periodPosting Date in format <Month,2><Month,2>|**Odb**|VAT Entry|Posting Date||
2|6|13|8|N|Posting date|format DDMMLLLL|**Dat knj**|VAT Entry|Posting Date||
3|15|22|8|N|OutputPosting Date|format DDMMLLLL|**Dat pre**|VAT Entry|Document Receipt Date||
4|24|53|30|AN|Document No.|the first 30 characters, left alignment|**Številka listine**|VAT Entry|Document No.||
5|55|62|8|N|Document date|format DDMMLLLL|**Dat lis**|VAT Entry|Document Date||
6|64|113|50|AN|Vendor name and address|the first 50 characters, left alignment|**Dobavitelj**|Posted document /Vendor /Customer|Pay-to Name, Pay-to Address, Pay-to City, Pay-to Country/Region Code||
7|115|134|20|AN|Vendor VAT registration No.|the first 20 characters, left alignment|**IŠ za DDV**|VAT Entry|VAT Registration No.||
8|136|151|16|N|The value of purchases of goods and services excluding VAT|right alignment, format -999999999999.99|**Vred brez DDV**|VAT Entry|Base|10, 11, 12, 13, 23, 111, 112, 4010, 4011, 4012, 4013, 4023, 4026, 4111, 4112, 5010, 5011, 5012, 5111, 5112, 29, 20, 30, 4020, 5020|Type: Purchase
|||||||||||18, 6023, 25, 26, 107, 108, 4108, 27, 6013, 4623, 4613, 6053, 6063, 4653, 4663|Type: Sale
9|153|168|16|N|The value of purchases of goods and services in Slovenia from reverse charge VAT|right alignment, format -999999999999.99|**Vred SAMOOBD**|VAT Entry|Base|5141, 5140, 5041, 5040, 41, 40, 141, 140, 42, 43, 5042, 5043, 5142, 5143, 142, 143, 4042, 4043, 4142, 4143, 44, 5044, 4041, 4040|Type: Sale
10|170|185|16|N|The value of purchases of goods from EU|right alignment, format -999999999999.99|**Vred PRID BLA**|VAT Entry|Base|130|Type: Purchase
|||||||||||311, 312, 313, 314, 4311, 4312, 4313, 4314, 5313, 317, 318, 5314| Type: Sale
11|187|202|16|N|The value of purchases of services from EU|right alignment, format -999999999999.99|**Vred PREJ STOR**|VAT Entry|Base|15, 16, 5016, 4016, 110, 109, 4110, 28| Type: Sale
12|204|219|16|N|The value of purchases of real estates excluding VAT|right alignment, format -999999999999.99|**Vred OBD NEPR**|VAT Entry|Base|5010, 5011, 5012, 5111, 5112, 5020|Type: Purchase
|||||||||||5313, 5314, 5016, 5141, 5140, 5041, 5040, 5042, 5043, 5142, 5143, 5044|Type: Sale
13|221|236|16|N|The value of purchases of fixed assets excluding VAT|right alignment, format -999999999999.99|**Vred OBD OS**|VAT Entry|Base|4010, 4011, 4012, 4013, 4023, 4026, 4111, 4112, 4020, 4653, 4663|Type: Purchase
|||||||||||4313, 4314, 4311, 4312, 4016, 4108, 4110, 4042, 4043, 4143, 4041, 4040, 4623, 4613| Type: Sale 
14|238|253|16|N|The value of exempt purchases and purchases in EU excluding VAT|right alignment, format -999999999999.99|**Vrednost ON**|VAT Entry|Base|8, 309, 4008, 4309, 5008|Type: Purchase
15|255|270|16|N|The value of exempt purchases of of real estates excluding VAT|right alignment, format -999999999999.99|**Vred OPR NEPR**|VAT Entry|Base|5008|Type: Purchase
16|272|287|16|N|The value of exempt purchases of of fixed assets excluding VAT|right alignment, format -999999999999.99|**Vred OPR OS**|VAT Entry|Base|4008, 4309|Type: Purchase
17|289|304|16|N|Undeductable VAT|right alignment, format -999999999999.99|**Neodbitni DDV**|VAT Entry|VAT Amount|10, 4010, 5010, 311, 312, 4311, 4312, 110, 107, 108, 109, 42, 43, 5042, 5043, 5142, 5143, 142, 143, 4108, 4110, 20, 4020, 5020, 4042, 4043, 4143, 11, 12, 5011, 5012, 4011, 4012, 29, 991, 992, 11, 5041, 5040, 41, 40, 4041, 4040, 4023, 4026, 23, 13, 314, 313, 5016, 4314, 4313, 4016, 16, 15, 4108, 26, 25, 5314, 6053, 6063, 4653, 4663|Type: Purchase
18|306|321|16|N|Deductable VAT 22%|right alignment, format -999999999999.99|**VST 22% DDV**|VAT Entry|VAT Amount|16, 314, 4314, 5314, 6023, 5016, 4016, 5141, 5041, 41, 141, 26, 12, 23, 112, 5012, 4012, 4023, 4026, 4112, 5112, 4041, 4623|Type: Purchase
19|323|338|16|N|Deductable VAT 9,5%|right alignment, format -999999999999.99|**VST 9,5% DDV**|VAT Entry|VAT Amount|15, 313, 4313, 5313, 5140, 5040, 40, 140, 25, 11, 13, 111, 5011, 4011, 4013, 4111, 5111, 4040, 6013, 4613, 30|Type: Purchase
20|340|355|16|N|Flate-rate compensation 8%|right alignment, format -999999999999.99|**Pav nadomestilo**|VAT Entry|VAT Amount|29|Type: Purchase
21|357|516|160|AN|Notes - not mandatory|left alignment|**Opombe**|VAT Entry|Posting date||
