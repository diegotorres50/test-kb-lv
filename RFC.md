# Contact Importer - Instructions

The objective of this exercise is to evaluate technical knowledge, use of good practices, and creativity when facing development problems. Good use of databases and testing will be taken
into consideration. The tasks will be presented in the form of user stories to facilitate the understanding of the exercise.

## Delivery format - Requiered: 

A link to a public repository on Github or Bitbucket which should include:

- A README file with instructions on how to run the software including a test user.
- At least one .csv file for testing multiple scenarios that you contemplated. The location of the .csv file(s) must be listed in the README file.

The application will allow users to upload contact files in CSV format and process them in order to generate a unified contact file. The contacts must be associated with the user who imported
them into the platform. When uploading the files, the application must validate that the fields entered are correctly formatted. You must take into account that the files can have many
records.

## The exercise consists of the following:

1. As a user, I must be able to log into the system using an email and a password.
2. As a user, I must be able to register on the platform. For this, it will only be necessary to enter a username and password.
3. As a user, I must be able to upload a CSV file for processing. At the time of uploading the file, the user must choose which column belongs to which specific contact
information, i.e. the user must match the columns of the file with the information to be processed and then save it into the database. This means that in the CSVs the columns
with information will not be standard and may arrive in a different order or with different names than the ones that will be used in the database.
4. The following values must be saved in the database:

    - **Name**
    - **Date of Birth**
    - **Phone**
    - **Address**
    - **Credit Card**
    - **Franchise**
    - **Email**
    
5. As a system, I must process the content of the CSV file. The following validations must have the elements in the CSV file
    - **Name**: Names with special characters, except for the minus(-) will be invalid values and cannot be saved.
    - **Date of Birth**: The system will only accept two types of ISO 8601 date formats (%Y%m%d ) and (%F). Any date that does not have these formats will not be
saved. At the end, the date must be displayed in the following format Year Month Day i.e. 1985 January 4.
    - **Telephone**: Valid phone formats are (+00) 000 000 00 00 00, for example (+57) 320 432 05 09. And (+00) 000-000-00-00, for example (+57) 320-432-05-09. Any
      number that does not comply with this format should be ignored.
    - **Address**: for the address there’s nothing to validate other than it’s not empty.
    - **Credit Card**: With the credit card two processes must be done. The first one is to obtain the franchise to which it belongs. For this we must use the IIN with the
      card numbers as explained [here](https://en.wikipedia.org/wiki/Payment_card_number#Major_Industry_Identifier_.28MII.29). In the table below you can see examples for each franchise in place. The second process is to encrypt the credit card number. For this you must validate that the length of the card is the corresponding for the franchise and then encrypt the number with a method that is not recoverable. You must remember that at the moment of showing the card on the final screen you must only show the last 4 numbers.
      
      | Credit Card Type | Credit Card Number |
      |------------------|--------------------|
      | American Express | 371449635398431    |
      | Diners Club      | 30569309025904     |
      | Discover         | 6011111111111117   |
      | JCB              | 3530111333300000   |
      | MasterCard       | 5555555555554444   |
      | Visa             | 4111111111111111   |
    - **Franchise**: The franchise must be identified from the credit card number.
    - **Email**: must have a valid email format and it can’t be repeated per associated account. This means that user A can have a contact example@gmail.com and user B can have the same contact example@gmail.com but neither user A nor B can have two contacts with the same email address repeated. Note that all columns are required.
6. As a user, I should be able to see a summary of the contacts I have imported. All contacts that I have imported and that were successfully created should be displayed in a list that is paginated.
7. As a user, I should be able to see a log of the contacts that could not be imported and
      the error associated with it.
8. As a user, I should be able to see a list of imported files with their respective status. Valid statuses include: On Hold, Processing, Failed, Terminated. The statuses are described as follows:
      
    - **On Hold**: the file has been uploaded but has not yet started processing.
    - **Processing**: the file is actually being read and performing the actions required above
    - **Failed**: not a single contact could be imported due to data errors (If the contact file is empty it should not be considered as failed).
    - **Finished**: the whole file has been processed and at least one contact has been registered in the database.
    -
9. **BONUS: Process the CSV file in a background job.**

## Observations:

When evaluating, we will not take the front-end as a priority. All that is requested in this
regard is that the information and navigation be presented in a clear and organized
manner. In that sense, this test must be able to be completed without the use of
Javascript, so the use of this is completely optional and at the discretion of the person
being evaluated. A framework such as Bootstrap can be used if desired.
