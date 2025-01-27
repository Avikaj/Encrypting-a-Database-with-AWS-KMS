# Encrypting-a-Database-with-AWS-KMS

## Introduction
This project demonstrates how to secure a database by implementing encryption using AWS Key Management Service (KMS). AWS KMS is a fully managed service that enables users to create and control encryption keys to protect data. In this project, we explore how to integrate KMS with a relational database, ensuring that sensitive data is securely encrypted both at rest and in transit.

## Project Layout
<img width="800" alt="Screenshot 2025-01-26 at 7 58 19 PM" src="https://github.com/user-attachments/assets/2f109e9d-924d-43f8-83a9-212c3ae4eb92" />

## Project Solution
### Step 1: Create an AWS KMS Key
1. Creating a Customer-managed key: Symmetric and Encrpyt and Decrypt for Key Usage.
<img width="1512" alt="Screenshot 2025-01-26 at 8 26 50 PM" src="https://github.com/user-attachments/assets/655f3568-565c-405f-9ec4-e1ceda2c51f4" />

### Step 2: Creating a DynamoDB Table and encrypting it
After creating a table with id as the partition key, this is how to choose the encryption key created before:
<img width="1512" alt="Screenshot 2025-01-26 at 8 30 52 PM" src="https://github.com/user-attachments/assets/7c96f30c-c094-48a0-96ec-99c6a669436e" />

### Step 3: Add data to the DynamoDB Table
This item is visible because of the "Transparent Data Encryption" feauture of DynamoDB where all the data is secured while accessible to the authorized users with appropriate permissions.( I am the IAM Admin User right now (as shown in Layout))
<img width="1512" alt="Screenshot 2025-01-26 at 8 35 41 PM" src="https://github.com/user-attachments/assets/904ee5d8-ee6f-4f4b-9786-5c58180030eb" />

### Step 4: Create a Test User
This helps us to confirm if the encryption is working or not, with limited permissions.
This user will have full access to DynamoDB.
<img width="1512" alt="Screenshot 2025-01-26 at 8 43 36 PM" src="https://github.com/user-attachments/assets/c13a9d4b-96cf-4acf-b99a-97d15ec42e27" />

### Step 5: Validating the Test user
Here, as there were not enough permissions for this user, they were denied access to the items of the same DynamoDB table.
Precisely, the error meesgae denies the user to "Decrypt", which is reversing the encryption done in earlier steps.
<img width="1508" alt="Screenshot 2025-01-26 at 8 47 18 PM" src="https://github.com/user-attachments/assets/e374bae7-587e-4296-ae1d-3fb366b3f355" />

## Extra: How is this way different from the other ways to control access?
Other access controls, like security groups limit the access to a resource(eg. DynamoDB Table) or an entire service(eg. DynamoDB). These don't protect the data inside these resources. If someone has access to the resources they can read and misuse the data.
With AWS KMS, the data within a resource is secured too. Even someone gains access, they will not be able to read or misuse the data until they have the decryption key.
This adds a layer of security i.e. Access permissions + Decryption keys.

Here, after adding the user to the KMS key:

<img width="1509" alt="Screenshot 2025-01-26 at 8 56 08 PM" src="https://github.com/user-attachments/assets/15cbb3d3-efd9-4ede-9fda-7790c6da59c9" />
This user can see the items in the DynamoDB Table.

<img width="1507" alt="Screenshot 2025-01-26 at 8 56 17 PM" src="https://github.com/user-attachments/assets/603a481a-6a7f-4949-a564-491a337960cf" />

