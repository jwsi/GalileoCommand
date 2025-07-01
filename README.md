# Automated Travel Platform (ATP) for GDS integration with AERTicket
 
## Introduction

This system is designed to serve as a complete travel management platform for small to medium sized agencies with Travelport Galileo GDS access utilising AERTicket UK as a consolidator. The system is purely script based and seamlessly integrates with Smartpoint Desktop and has the following core features:

- Management of traveller profiles including
	- Profile Name
	- Full passenger name
	- Passport Info (Secure DOCS)
	- Date of birth
	- Phone Number
	- Email
	- Frequent flier (mileage) information
- Creation, modification and deletion of traveller profiles
- Automated SSRDOCS entry into PNRs
- Automated AERTicket directive entries required for ticketing
- Automated distinguisher for private and public fares
- Automated age calculation for infants and children
- One-command holding
- One-command ticketing / queueing 
- One-command cancelling
- One-command PNR division
- One-command profile listings
- One-command PNR fare reinstatement
- One-command PNR refresh

The entire system is accompanied with easy to use graphical interfaces and takes the complexity away from handling traditional Galileo cryptic commands. The entire platform takes around 10 minutes to install and from that point on you have a system that can serve as your management backbone for your travel platform. This system is also able to work across multiple terminals connected to the same PCC by virtue of it using PCC client files as its core database.

## Prerequisites & Installation

Before using the system you must have:

- An agreement in place with AERTicket UK including a selective access agreement between your PCCs and theirs. This agreement must allow you to queue PNRs onto AERTicket's PCCs
- Access to Smartpoint Desktop on Windows.
- An agency file conforming to the format defined in `./formats/agencyfileformat.txt`
- A new business file called `ATP` that conforms to the format defined in `./formats/businessfileformat.txt`
- Masking removed by Travelport for your PCC.
- The ability for your GDS users to add and modify client files.
- The ability to delete client files for an admin user on your GDS account if and only if you wish to delete traveller profiles.

#### Installation

1) Download the repository as a zip file.
2) Extract the file.
3) In Smartpoint Desktop open up the Smart Buttons menu (it has a "SB" icon).
4) Click import.
5) Browse to the scripts located within the extracted files you just downloaded and add each script one at a time.
6) When this is finished you should have all the scripts shown in your Smart Buttons menu.

The installation is now complete!

## Usage

Each of the scripts is designed to perform a unique and useful function and can be invoked by either clicking the Smart Button in question or typing the script name into the GDS terminal. E.g. typing `ADD` will run the ADD script. The excerpts below provide an abstract overview of each of the scripts functions:

- `CREATE` - This creates a new traveller profile. It will bring up a user-friendly GUI to allow one to enter traveller information. Note that the name of the traveller profile need not equate to the full name of the traveller and can conform to whatever format you desire for your organisational needs.

- `EDIT` - This edits an existing traveller profile. It will bring up a user-friendly GUI to allow one to modify existing traveller information.

- `DELETE` - This deletes an existing traveller profile. It will bring up a text prompt for the name of the traveller profile one wishes to delete. Please note that this can only execute successfully if the user in question has permission to delete client files.

- `LIST` - This lists all existing traveller profiles that are stored by the automated travel platform (ATP).

- `ADD` - This brings up a GUI for entering a traveller profile name. Once entered it will add all relevant information for that traveller into the PNR including name, SSRDOCS, mileage information and so on.

- `HOLD` - This will hold all segments in the currently displayed PNR and request the creation of a vendor locator for the PNR. *This must be done prior to any ticketing operation.*

- `REFRESH` - This simply refreshes the PNR to ensure the most up to date information is displayed.

- `REINSTATE` - This reinstates expired fares for the PNR. This is useful if a segment has been held and then the fare expires. This reinstatement command must be executed if the filed fare for the PNR has expired.

- `TICKET` - This automatically adds in AERTicket UK directives for ticketing into the notepad, determines whether the fare is private or public and then submits to the ticketing queue at AERTicket.

- `DCPAY` - This organises payment and booking for all direct carriers (EasyJet, RyanAir etc...). This should be executed once all segments are present in the PNR.

- `DIVIDE` - This brings up a GUI which allows a user to select which passengers to divide out of the existing PNR. This is a useful command when travellers itineraries are no longer identical and need to be changed separately. Upon successful execution, a new linked PNR will be created for the divided passenger.

- `CANCEL` - This cancels all segments and fares in the currently open PNR.

- `SEATX` - This cancels all seat reservations for all segments in the PNR.

- `BAGS` - This adds extra bags for passengers on specific segments in the PNR if purchases cannot be made via ancilliary services.

## Issues/Problems

Please open issues in this repository for any operational issues or bugs experienced with this platform.

## Contributing

1) Please fork the repository.
2) Create a new feature branch in your forked repository.
3) Make your changes.
4) Make a Pull Request back into the main branch on this repository, the changes will then be reviewed.
