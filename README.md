# Encrypt-Data-with-AWS-KMS
In this project, I will demonstrate using encryption to secure data. The goal is to create encryption keys using AWS Key Management system ( AWS KMS ), encrypt a DynamoDB table's data with that key, then test access using IAM users. 


# Encrypt Data with AWS KMS

**Author:** Darryl Brown  
**Email:** darrylbrown1991@gmail.com

---

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

In this project, I will demonstrate using encryption to secure data. The goal is to create encryption keys using AWS Key Management system ( AWS KMS ), encrypt a DynamoDB table's data with that key, then test access using IAM users. 

### Tools and concepts

Services I used include AWS IAM, AWS DynamoDB, AWS KMS (Key Management Service). Key concepts I learnt include encryption, data base tables, KMS using permission to actions rather than just access to the key itself, and creating a user to test access.

### Project reflection

This project took me approximately 30 minutes. The most challenging part was understanding how encryption works differently than other access controls. It was most rewarding to see how I was able to give test user access to table in DynamoDB.

I chose to do this project today because get hands on with AWS DynamoDB and cloud security best practices, getting more exposure with encryption and encryption keys, and managing access as an administrator. 

---

## Encryption and KMS

Encryption is the process of that uses algorithms to convert data into a secure format called ciphertext. Only authorized users can decrypt and restore the data to its original, readable state. Companies and developers do this to secure user data, transactions, files and more. During the encryption process, the encryption algorithm reads an encryption key. This key tells the algorithm exactly how it would transform plain text into the jumbled up format called cipher text. For example, the key could tell the algorithm to swap out certain parts of the data or shuffle the order of data to break up patterns.

AWS KMS is secure vault for my encryption keys.  Key management systems are important because you can use them to create, manage, and use encryption keys that protect the data in your AWS resources.

Encryption keys are broadly categorized as symmetric and asymmetric. I set up a symmetric key because I'll be using the exact same key to encrypt and decrypt my data.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is one of AWS's database services. DynamoDB stands out as a fast and flexible way to store my data, which makes it a great choice for applications that need quick access to large volumes of data. A partition key is the heart of how DynamoDB organizes data. Think of it as a label that you can use to group similar items. Under the hood, the partition key is how DynamoDB spreads out your data across different servers for quick access and efficient querying.

The different encryption options in DynamoDB include AWS owned key, AWS managed key, and Customer managed key. Their differences are based on who creates and manages the key and whether who has visibility. I selected the Customer Managed key ( CMK ) option to use my created key.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Rather than controlling who has access to the key, KMS manages user permissions by controlling the actions that people can do with that key. In my case even if I gave my test user the permission to see the key it would need permission to decrypt.

Despite encrypting my DynamoDB table, I could still see the table's items because transparent data encryption. DynamoDB uses transparent data encryption, DynamoDB is designed to decrypt the data on your behalf. When data is requested by an authorized user (like me) or an authorized application, DynamoDB retrieves the encrypted data, decrypts it with the key, then shows me the decrypted format so I can use it instantly. This security feature is called transparent data encryption. Transparent data encryption makes sure that my data is secure at rest, yet still accessible to authorized users that have the right permissions.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I configured a new IAM user to validate whether unauthorized user can access my encrypted data. The permission policies I granted this user are DynamoDBFullaccess but not encryption and decryption. 

After accessing the DynamoDB table as the test user, I encountered "Access denied to kms:Decrypt" because this user does not have access to encrypt or decrypt data.  This confirmed encryption keys can be used to secure data.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user use the encryption key, I added test IAM user to one of the Key users for the encryption key My key's policy was updated to two IAM users at the encryption key users.

Using the test user, I retried accessing the DynamoDB table. I observed that the user can see the data that is inside. Which confirmed that making it a key user is an affective way to authorize someone to see encrypted data.

Encryption secures data instead of an entire resource or service. I could combine encryption with other access tools like security groups and permission policies to have two layers of security, the resource level and then the data level.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-security-kms_feffb2fb8)

---

---
