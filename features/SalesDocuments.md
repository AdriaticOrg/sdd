# Sales Documents

Printable documents must meet local legislation. This feature resolves some missing fields from reports.

## Scope

Additional fields on printout of Sales Documents: Sales Invoice, Sales Credit Memo and shipment
- Place of Issue
- Date of Issue
- Shipment Date
- VAT Registration No. for customer
- VAT Date 
- VAT specification (also informative VAT)

## Architectural Design 

## Data Design

## Data Flow

Field|Source
-|-
Place of issue|Program transfers data from field City specified on Company Information.
Date of issue|Program transfers data from field Document Date on sales header.
Shipment Date|Program transfers data from field Shipment Date on sales header.
VAT Registration|Program transfers data from field VAT Registration No. on Customer Card.
VAT Date|Program transfers data from field VAT Date on sales header.
VAT Specification|Program calculates specification for each VAT % from sales header lines.

## User Interface

New fields on reports Sales Invoice, Sales Credit Memo and Shipment.

