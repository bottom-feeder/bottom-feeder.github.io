# Digital Signatures in Russia and in general. Theory and Practice 


In our new product, we plan to use digital signatures. 

This document covers the following topics:

* Basic concepts behind digital signatures. 
* How to create, obtain and use digital signatures in Russia.

At the end of the topic, you can find step-by-step instructions to generate and verify a mock-up Advanced electronic signature.

<br/>
# 1. General Information

A digital signature attached to an electronic document is a convenient and reliable alternative to a traditional handwritten signature. This type of signature doesn't require the physical presence of a signer and comes with a built-in forgery prevention mechanism.

As is with its traditional counterpart, the main purpose of the digital signature is to ensure the following:  
  
* The document is issued by its original author, and not someone with a fake identity;  
* The document contents weren't altered after the moment of its signature.  

Moreover, the digital signature guarantees that the received document is intact in terms of data integrity.

<br/>
The mechanism of the digital signature relies on the following concepts:

1. Public-key infrastructure (PKI);
2. Hashing algorithm;
3. Certificate authority.

<br/>
## 1.1 Public-key Infrastructure (PKI)

Cryptographic keys perform encryption based on a chosen algorithm or cipher. While the algorithms are the general principles or rules used by a given cryptosystem, the keys are what actually perform the function.

In PKI the keys are generated in pairs. The key pair consists of a *private* (also called *secret*) key and a *public* key. Each of the two interacting parties uses separate keys—one for encryption and a different one for decryption. The encryption key is the public key and the decryption key is the private key.

The main idea is that both keys are interrelated and complementary. The picture below details the generation of the key pair.

![Public key genration](https://i.ibb.co/FmxhSFh/Public-key-generation.png)

The basic idea behind public-key cryptography is that only one of the two keys needs to be kept secret. The other key, the public key, is designed to be available to everyone, hence the name. 

It may seem a bit counter-intuitive, but this has a solid mathematical basis. For example, anyone can compute the product of 113 and 293 and get the correct answer of 33,109. It is much more difficult to work a similar problem in reverse: e.g., which two whole numbers, when multiplied, produce 29,213?
  
  
<br/>
The figure below shows how public-key encryption can work: 

* Party A, depicted on the right as a server, generates two keys and publishes the public one. It doesn’t disclose the private key.  
* Party B, depicted on the left as a laptop, gets a public key from Party A and enciphers plaintext ("Hello") with it.  
* Party B sends the encrypted message.  
* Party A deciphers ciphertext ("y6uW$I") with its private key. Since only Party A has the private key, only it can successfully decrypt the information.  

![How public encryption works](https://i.ibb.co/JtynNHr/How-keys-work.png)		

<br/>
## 1.2 Hashing Algorithm

Since the transferred document or message could be of any size, it is impractical to encrypt large files and too risky to encrypt small files, since they are easier to decrypt. A workaround is a special type of cryptographic function known as a *hash function*. A hash function creates a special mathematical summary of information. This summary is of fixed size, usually 256 or 512 bits, depending on the hashing algorithm. If someone modifies the information and the hash function is recalculated, it will give a different summary. Cryptographic hash functions resemble checksums or cyclic redundancy check (CRC) codes.

The picture below illustrates how hashing works.

![How hashing works](https://i.ibb.co/CnrspDN/Hashing.png)  

<br/>
## 1.3 Signing and Verification. Certificate Authority

The digital signature of a document is the hash of the data from the document encrypted with a sender's private key. This type of signature is called the Advanced electronic signature (AdES). AdES has the following properties:

* It contains information about the signer: name, e-mail address, and other details.
* It originates from the person in possession of a private key.
* It captures the state of data at the moment of signature, i.e. could reveal the fact of tampering with signed data.

<br/>
The receiving party (the verifier) must check the signature validity. The verification procedure follows the following steps:

1. The verifier receives the document along with a digital signature.  
1. The verifier gets the signer's public key and decrypts the signature with it.
1. The verifier applies the same hashing algorithm as the signer to the document.
1. The verifier compares the calculated result with the hash from the decrypted signature. If the hashes match, the signature is valid.

![How hashing works](https://i.ibb.co/sqFPQ05/Signing-and-verifying-Ad-ES.png)  



However, a malicious agent in the middle of the exchange can theoretically intercept the public key and signed data, replacing it with their key and fraudulent data. To prevent this, a third party, both the signer and verifier can trust, known as the Certificate Authority (CA), guarantees the validity of the digital signature. To accomplish this, the CA checks the signer's identity, usually presented in hard-copy form, and verifies their signature. If everything looks good, the CA issues a Digital certificate for the signature. This certificate contains the public key for a digital signature and specifies the identity associated with the key, such as the name of the signatory's organization.

AdES with a Digital certificate is known as the Qualified electronic signature.

<br/>
# 2. Digital Signatures in Russia

## 2.1 General information
Russian digital-signature (DS) system is based on European eIDAS (electronic IDentification, Authentication and trust Services). Russian Federal Law 63-FZ regulates the use of DS in the Russian Federation. 

A mandatory requisite for legally significant documents is a DS that complies with a Bank of Russia industry standard for information security (STO BR IBSS). Algorithms used to create and verify DS for payment orders, cash orders, payment requests, and other financial documents must comply with the Russian industry standards (GOSTs). All cryptographic software must be certified in Russia. This requirement practically prevents the use of any foreign software.

GOST R 34.10-2012 describes the mathematical requirements for the signature signing and verification processes. The standard is open and free to use, however available only in Russian.

## 2.2 Three types of DS
63-FZ categorizes all DS into the following types:

1. Simple DS.
2. Unqualified enhanced DS.
3. Qualified enhanced DS. 

 
### 2.2.1 Simple DS
 Essentially a username and a password. This type of DS does not allow validating the author's identity and the data integrity, but still provides some protection. This is the simplest and least expensive DS to obtain. Simple DS is used for authentification on government-run websites and certain other commercial services. Simple DS does not bear a legal value as a handwritten signature unless the parties agreed on this during personal interaction.  

 You can create a Simple DS yourself, using non-cryptographic software like *MS Word.*
 
### 2.2.2 Unqualified enhanced DS

  A Russian counterpart of eIDAS-regulated AdES. This signature verifies the identity of the author and protects the contents of the document from subsequent modifications. Unqualified enhanced DS can be used instead of wet-ink signature in bilateral B2B or B2C communication by mutual agreement of the parties.  

 You can create unqualified enhanced DS yourself using any available cryptographic software, like an *Adobe Acrobat CryptoPro* plug-in, or open-source software like *Gpg4win* and *Kleopatra*.

### 2.2.3 Qualified enhanced DS

 A Russian counterpart of eIDAS-regulated Qualified electronic signature. It is Unqualified enhanced DS that received authorization from the state-accredited Certificate authority and was created with government-approved cryptographic software and hardware. Qualified enhanced DS requires a digital certificate issued by CA. The certificate is uploaded to a *token*—a government-approved USB drive with copy protection. Practically, this type of signature can be used instead of a handwritten signature for government procurements and when communicating financial data to government agencies like tax offices or pension funds, or private-owned Russian and foreign companies.  

 To obtain Qualified enhanced DS you must submit a list of identification documents to a local accredited CA and pay a certain fee. You will receive the certificate and keys on a token. The certificate is valid for 1 year and requires renewal after that period.




<br/>
# 3. Creating and Verifying AdES

Practice signing and verifying DS with the encrypting command-line tool [GNU Privacy Guard (GPG)](https://gnupg.org). GPG comes built-in in most Linux distributions. For other OS, download PGP from [gnupg.com](https://gnupg.org/download/index.html). 

This section describes how to generate and verify DS in GnuPG/MacGPG2 2.2.32 + libgcrypt 1.8.8 on a Unix-based OS.

<br/>
## 3.1 Generating a Key Pair
*To generate a key pair:*  

1. Open the command line;

2. Type `gpg --full-generate-key`;

3. Choose cryptography parameters;
 >Note. You can select default parameters by pressing **Enter** without typing anything.  

4. Confirm validity period, if prompted;
5. Provide your name, email address (optional), and comment (optional);
6. Review your choices and press **O**;
7. Choose a passphrase to protect your keys.

After confirming the passphrase you will get the following message:  

	gpg: key C273E1B8B9725BBE marked as ultimately trusted
	gpg: revocation certificate stored as '/Users/john/.gnupg/openpgp-revocs.d/014B757EA6E95BD96FF7CE61C273E1B8B9725BBE.rev'
	public and secret key created and signed.

	pub   rsa3072 2021-11-22 [SC]
      014B757EA6E95BD96FF7CE61C273E1B8B9725BBE
	uid                      john
	sub   rsa3072 2021-11-22 [E]

  where *john* is your ID of choice.
  
  <br/>
To export the public key into a shareable and readable format, type `gpg --export -a "john" > public.key`,
 >Note. The *.key* file will be exported to your default directory.  
 
where *john* is your ID of choice.
	
<br/>
To export the secret key into a readable format, type `gpg --export-secret-key -a "john" > private.key`,

> Note. Never share your secret key with anyone.
 
where *john* is your ID of choice.

 <br/>
## 3.2 Signing the Document
To digitally sign a document with a signature, type `gpg -ba "document.doc"`,
	
  where *document.doc* is the name of the file to be signed.

> Note. If the file to be signed is not in your default directory, include the full path.
 
The command creates a signature file with an extension *.asc* at the directory with the signed file. For a signed file with the name *document.doc*, the command generates signature file *document.doc.asc*. You can change the extension to *.sig*, if you like.

<br/>
## 3.3 Verifying the Signature
To verify your own signature, type `gpg --verify "document.doc.asc" "document.doc"`,

where *document.doc.asc* is the signature file, and *document.doc* is the signed file.

<br/>
If the signature is valid, you will get the following message:

	gpg: Signature made Mo 22 Nov 01:02:27 2021 MSK
	gpg:                using RSA key 7FFEDF970426E372482491005D7E0B382F728D37
	gpg: Good signature from "john" [ultimate]
where *john* is your ID of choice.

<br/>
*To verify the signature of someone else:*

1. Obtain the public key.  
2. Import the public key to your local keystore by typing `gpg --import "public.key"`   
3. Obtain the signature file.  
4. Type `gpg --verify "signature.sig" "document.doc"`,  

where *public.key* is the obtained public key, *signature.sig* is the obtained signature file, and *document.doc* is the signed document.

 
<br/>
Please note that PGP doesn't support GOST-approved algorithms. To enable its support, activate the GCrypt-1.7.0 library. See the details at [habr.com](https://habr.com/ru/post/316736).

 


