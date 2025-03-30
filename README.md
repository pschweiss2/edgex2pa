# edgex2pa
Connecting Ricoh EdgeXperience Capture Service to Microsoft Power Automate
</p>
<p style="font-size: 32px;" align="center"><strong>A Community guide on using the Ricoh EdgeXpereince Capture Service native SharePoint connector to enable Microsoft Power Automate</strong></p>
<hr style="border: 2px solid black; width: 50%;">


### Support My Work

If you find my work helpful, feel free to buy me a coffee!

[![Buy Me a Coffee](https://www.buymeacoffee.com/assets/img/custom_images/yellow_img.png)](https://www.buymeacoffee.com/petes)


### A little bit of background
We deployed Ricoh's EdgeXperience Capture Service to solve for a number of opportunites we had in our environment. One of those was the need to get paper records into Salesforce in the most secure manor possible and eliminate shadow copies created by tradition scan to email, download, upload. *Full disclosure* I am certain there is probably more efficient way to do this on the Power Automate side, I welcome and appreciate any feedback! I beleive in the power of communtiy on projects like this and would love to collaborate with anyone who would like contribute. 

### Here's the nuts and bolts of the project.
Before we get to the How To, here's a couple of items I am working to figure out in future iterations of this.
* In the next iterartion instead of tieing each file to a record on ingest, it will be tied to the individual, and Salesforce Agentforce will suggest where to route the file. Allowing the user to accept the suggestion or identify a different location.

* ### Now the good stuff! 

### 1) You'll need a location in SharePoint for the initial scanned documents to land.
In my use case I just created a team site that had a single document library setup. If you have a functional site already you could use that! Just needs to have a document library.

### 2) Setup the job in EdgeXperience
Build a standard SharePoint job, and make sure you ask the end user to input a Scan ID (more on how to generate this later!). 
![image](https://github.com/user-attachments/assets/45e92a14-aa87-4616-998f-62b2c5d77d48)
### You'll want the scan ID to be at the beginning of the file name followed by a single underscore.
![image](https://github.com/user-attachments/assets/56b98a6c-a885-42f6-a844-942afb09ea2e)

That's it for the EdgeXperience job, feel free to include any other variables you may want on the end of the file. 

### 3) Junction between EdgeXperience and Salesforce
I created a simple object in Salesforce that essentailly is a junction between EdgeXperience and Salesforce. The record has just a few fields, enough to connect the two records. The functional fields are the Scan ID (an autonumber field unique to each record) and the destination record (where the file should go!)
![image](https://github.com/user-attachments/assets/3e9da9ac-bf96-4a78-9e43-a766f4763cec)

### 4) Creating the UX
To bring this all together we will employ Salesforce Flow to present the scan ID to the user.
The flow is relativly simple, you present the users with a screen that generates a 6 digit pin. A junction record is then created that links that pin to the Salesforce record. 

![image](https://github.com/user-attachments/assets/d4b0b824-127b-450e-b7d5-005eaad57a98)

### 5) Ingest the document
Invoke your newly created Scan2Salesforce job on the scanner interface and enter the Scan ID we got from Salesforce. Feed the document and EdgeXperience will take the images in and begin the image clean up process, eventually dropping the files off in the SharePoint library we created in step 1. Now it's up to PowerAutomate to take the the file from SharePoint and send it off to Salesforce.
![image](https://github.com/user-attachments/assets/0cedca09-9c5f-4255-8a39-36c34f490542)







