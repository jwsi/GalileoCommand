# Galileo Command (GC)
 
## Introduction

This system is designed to serve as a complete travel management platform for small to medium sized agencies utilising Travelport Galileo GDS. Out of the box it is designed for integration with AERTicket UK as a consolidator. The system is purely script based and seamlessly integrates with Smartpoint Desktop application and has the following core features:

- Management of traveller profiles including
	- Profile Name
	- Full passenger name
	- Passport Info (SSRDOCS / APIs)
	- Date of birth
	- Phone Number
	- Email
	- Frequent flier (mileage) information
- Creation, modification and deletion of traveller profiles
- Creation of cost centres and association of traveller profiles within cost centres
- Propagation of cost centre names to AERTicket UK invoices
- Automated SSRDOCS / API entry into PNRs
- Automated AERTicket directive entries required for ticketing
- Automated distinguisher for private and public fares
- Automated age calculation for infants and children
- One-command holding
- One-command ticketing / queueing 
- One-command cancelling
- One-command PNR division
- One-command seat cancellation
- One-command direct payment carrier booking
- One-command PNR fare reinstatement
- One-command PNR refresh

The entire system is accompanied with easy to use graphical interfaces and takes the complexity away from handling traditional Galileo cryptic commands. The entire platform takes around 10 minutes to install and from that point on one is in posession of a system that can serve as your management backbone for your travel platform. This system is also able to work across multiple terminals connected to the same PCC by virtue of it using PCC client files as its core database backend.

## Prerequisites & Installation

Before using the system you must have:

- An agreement in place with AERTicket UK including a selective access agreement between your PCCs and theirs (specifically AERTicket PCC 74QP). This agreement is required to faciliate queueing PNRs onto AERTicket's PCCs for ticketing. It must be fully permissive.
- Access to Smartpoint Desktop on Windows with valid login credentials to Galileo GDS.
- An agency file conforming to the format defined in `./formats/agencyfileformat.txt`. See agency file setup below for more info.
- Masking removed by Travelport for your PCC.
- The ability for GDS users to add and modify client files.
- The ability to delete client files for an admin user on your GDS account if and only if you wish to delete traveller profiles.

#### Agency File Setup

1) Execute `C*` to show the current agency file.
2) Execute `C@1N/AGENCY_NAME` where you replace `AGENCY_NAME` for your travel agency.
3) Execute `C@2Y/P.LONT*01432123456` where you replace `01432123456` with your agency's landline telephone number.
4) Execute `C@3Y/F.S` to ensure all PNRs made by GC are set as cash payment.

### Installation

1) Download the repository as a zip file.
2) Extract the file.

#### Cost centre file setup

Traveller profiles are located within cost centres. These cost centres are created automatically by GC. In order to set these up specific to your agency, edit `CREATE CC.xml` within the scripts folder. Lines 9-13 should be replaced with your travel agency information.

#### AERTicket Customer Number setup

To ensure billing is correct, ensure your AERTicket customer number is submitted on PNRs when ticketing. To do this, edit TICKET.xml in the scripts folder. Set `CUSTOMERNUMBER` on line 32 to be your AERTICKET customer number.

#### Installing SB Scripts

3) In Smartpoint Desktop open up the Smart Buttons menu (it has a "SB" icon).
4) Click import.
5) Browse to the scripts located within the extracted files you just downloaded and add each script one at a time.
6) When this is finished you should have all the scripts shown in your Smart Buttons menu.

The installation is now complete!

## Usage

Each of the scripts is designed to perform a unique and useful function and can be invoked by either clicking the Smart Button in question or typing the script name into the GDS terminal. E.g. typing `ADD` will run the ADD script. The excerpts below provide an abstract overview of each of the scripts functions:

- `CREATE cc` - This creates a new cost centre to house traveller profiles. It will bring up a user-friendly GUI to allow one to enter a name for the cost centre in question. This could be a downstream client such as COMPANY X. This cost centre name will propagate through to AERTicket invoice PDFs.

- `CREATE PERSON` - This creates a new traveller profile. It will bring up a user-friendly GUI to allow one to enter traveller information. Note that the name of the traveller profile need not equate to the full name of the traveller and can conform to whatever format you desire for your organisational/referencing needs.

- `EDIT` - This edits an existing traveller profile. It will bring up a user-friendly GUI to allow one to modify existing traveller information.

- `ADD` - This brings up a GUI for entering a traveller profile name. Once entered it will add all relevant information for that traveller into the PNR including name, SSRDOCS, mileage information and so on.

- `HOLD` - This will hold all segments in the currently displayed PNR and request the creation of a vendor locator for the PNR. *This must be done prior to any ticketing operation.* This script also adds in SSRDOCS for passengers in question in formats specific to each segment.

- `REFRESH` - This simply refreshes the PNR to ensure the most up to date information is displayed. It is executed automatically after holding to ensure vendor locator information is included on the PNR.

- `REINSTATE` - This reinstates expired fares for the PNR. This is useful if a segment has been held and then the fare expires. This reinstatement command must be executed if the filed fare for the PNR has expired.

- `TICKET` - This automatically adds in AERTicket UK directives for ticketing into the notepad, determines whether the fare is private or public and then submits to the ticketing queue at AERTicket.

- `DCPAY` - This organises payment and booking for all direct carriers (EasyJet, RyanAir etc...). This should be executed once all segments are present in the PNR. It allows for direct payment via AMEX cards and itinerary information and receipts will go to the email address defined on line 11 in CREATE CC.xml.

- `DIVIDE` - This brings up a GUI which allows a user to select which passengers to divide out of the existing PNR. This is a useful command when travellers itineraries are no longer identical and need to be changed separately. Upon successful execution, a new linked PNR will be created for the divided passenger.

- `CANCEL` - This cancels all segments and fares in the currently open PNR.

- `CANCEL SEATS` - This cancels all seat reservations for all segments in the PNR.

## Issues/Problems

Please open issues in this repository for any operational issues or bugs experienced with this platform.

## Contributing

1) Please fork the repository.
2) Create a new feature branch in your forked repository.
3) Make your changes.
4) Make a Pull Request back into the main branch on this repository, the changes will then be reviewed.
