# FamSos
Stay safe and connect globally
README.md

This is version 0.1 for blockchain based FAMSOS web app.  With the intention to come to the aid of millions of people in case of all types of emergencies. FAMSOS can be used to share critical data to authorities on time.

Current version takes care into account three emergency services (Police, Ambulance, Fire). Be a user or a service personnel, each person is expected to register with the app first using their ethereum account.

Registration Steps for User:
Login to metamask using your ethereum account. In case you hold multiple accounts, ensure that the account you use while registering should be set as the first account for using the services.
Click on ‘User Registration’.
Enter your name, and contact number. With static location in the current phase, the next phase would include dynamic fetching of user’s real time location.  After entering, click on sign up. (PLEASE ENSURE METAMASK GASPRICE IS SET TO 2 GWEI AND NOT 2e9 WHEN USING LOCALLY DEPLOYED CONTRACT. ALSO CHECK THE PLUGIN MANUALLY IF POP-UP DOESN’T HAPPEN.)
Go to ‘SOS tab in need of emergency.
Three simple buttons for the services, click on the one you need, and your SOS call would be visible to your nearest service personnel.

Registration steps for Service personnel:
Login to metamask using your ethereum account. In case you hold multiple accounts, ensure that the account you use while registering should be set as the first account for using the services.
Click on ‘Service Registration’.
Enter your name, and service type (Police, Ambulance, Fire). (Enter the service type in the given sentence case.) Static location for now. (PLEASE ENSURE METAMASK GASPRICE IS SET TO 2 GWEI AND NOT 2e9. ALSO CHECK THE PLUGIN MANUALLY IF POP-UP DOESN’T HAPPEN.)
You can see the request of the user nearest to you who might require your service, by clicking on the ‘Service’ tab.

Note: Future versions would include role-based views and once you register, you’d only see your required view as per role (User/Service).

Track Tab:
For easier management, all the registrations/requests/SOS service assigned to, would be visible here (contract storage updates, basically).

This project has been built as per following specifications.

Softwares/Libraries used:

Truffle : for contract creations and builds.
Ganache-cli: as the ethereum client which creates default 10 accounts with test ethers.
Metamask chrome plugin: as the ethereum wallet
Node and npm (as requirement for truffle and also for the UI (lite-server package to deploy UI))
Built on OS: Ubuntu 16.04 (64-bit) in virtualbox VM.

Steps to build and test the demo:
After installing the ganache-cli and truffle globally on ubuntu, create the project folder.
Initialize truffle (truffle init)
Create the contract (.sol file) under the newly-created contracts folder by truffle.
Add the migration script in the migration folder to deploy the contract.
Set the truffle.js file to specify the network parameters (host, port, network-id).
Install own3d ethPM package which is imported in the main contract (truffle install own3d).
Start ganache-cli with specific network-id (should be same as truffle.js file or to check all networks use “*” in the file)and copy the created account details along with 12 word seed to a .txt file (would be required while importing accounts to metamask).
Run truffle compile to compile the contracts, run truffle test to run the tests, and then truffle migrate to deploy.
Capture the famsos contract address and update the same in these files :- src/js: main.js, helpad.js and regserver.js- at the contract address after abi and all the functions’ ‘to’ parameter in these files).
Since this is being tested on one machine with one metamask, for ease of use, the above given files also have user address parameter which should be updated to have different account for each individual (be a user or service personnel).
Changes in helpad.js (after truffle migration, copy famsos address and insert at contract address after abi definition, parameter ‘to’ in functions setpol(), setamb(), setfire())
web3.eth.accounts[id] parameter (used in functions) should be same in main.js and helpad.js but different id in regserver.js at any point in time.
Changes in main.js (after truffle migration, copy famsos address and insert at contract address after abi definition, parameter ‘to’ in function reguser())
Changes in regserver.js (after truffle migration, copy famsos address and insert at contract address after abi definition, parameter ‘to’ in function regserver())
Use ‘npm run dev’ to launch the site on chrome (localhost:3000) with metamask installed.
(PLEASE ENSURE METAMASK GASPRICE IS SET TO 2 GWEI  AND NOT 2e9. ALSO CHECK THE PLUGIN MANUALLY IF POP-UP DOESN’T HAPPEN.)
Eg. To test, after importing 3 accounts in metamask (0,1,2), register web3.eth.accounts[0] in main.js and helpad.js as a user, web3.eth.accounts[1]as service personnel 1 and web3.eth.accounts[2] while registering service personnel 2. (In real scenario, these settings can be avoided by enforcing the user to always use their registered account as account 0). The (x,y) parameters in functions defined are the (latitude,longitude), change them each time while registering a different individual (dynamic location fetch in next phase). Raise the SOS call while being in user account and check the ‘Track’ to see which service personnel was allocated the request as per the location distance. The service personnel (while being in their account) can see who’s requested their service.

Handling emergency:
Currently a Kill contract button is provided on Track tab which kills the contract. This can be invoked only by contract’s owner account. After invoking this, one cannot invoke any other contract functions.

Immediate enhancements:
All service type options in a dropdown menu and allowing new service type to be registered. 
Dynamic location fetch while registering and during SOS call.



