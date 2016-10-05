# Universal CCD
### disthealth_eHealthWallet

Our blockchain entry into the #disthealth #hackathon

# Links
* [Our Presentation on our proposed solution](https://docs.google.com/presentation/d/16kK7OJzINItUhMO_3toGFg3vpAs3yIDP1l5XXYZWGZQ/edit?usp=sharing)

# Design Considerations
* IPFS is used for Public Distributed Storage
	* IPFS files never go away
	* Due to this current limitation, this solution would use the Private Swarms and Private Gateways currently being developed
	* We cannot trust IPFS, so we use a non-repudiation system like Tierion
* A Patient establishes a smart contract with their Payer (Insurance Company), who acts as their **Custodian**
	* This is akin to an Insurance Card you get today from your Insurance Company
	* The Custodian creates an empty **Ledger** in IPFS for the Patient
	* The hash from that Ledger file added to IPFS provides the original value in the User's digital eHealth wallet
		* The Patient's wallet also contains the Public Key of the Custodian
		* The Custodian retains the Patient's Public Key
* A Patient establishes a relationship with a Service Provider (Hospital)
	* This is akin to giving them their Insurance Card
		* This includes the Patient's Public Key
		* This includes the hash (Filename) for the Patient's Consolidated CCD Ledger file in IPFS
		* This includes the Custodian's Public Key
	* The Service Provider (SP) provides the Patient with the SP's Public Key that is added to the Patient's wallet
* A SP (Hospital, Clinic, Doctor, etc) contributes new CCD information for a Patient by adding the CCD into IPFS
	* The hash from the new file is added to the user's Ledger in IPFS
	* This is tracked as a Business transactions with the Custodian for the CCD addition added to IPFS using Ethereum
	* Values returned from the interactions with IPFS and Ethereum are used in a transaction with Tierion (which creates a verifiable record of any data or business process on the blockchain) 
* The same process as above, is used when Custodian's (most likely in a Case Management Situation) create additional data for a new CCD file.

# Smart Contract
Our smart contract between the User (Patient) and their Payer (Insurance Company), who acts as their Custodian, has the following features.

* Automatic Exchange Policies
* Digital Signatures
* Enforce Encryption Algorithms
* Enforce Key Size
* Key Exchange
* Licenses
	* Ability to submit data for research purposes that is stripped of PHI (anonymized)
* Protocols for Consolidated CCD
* Selective Sharing
* Version Information for Supported C-CDA format.

# Technologies Used

* [HealthLX CCD viewer (Patient Insight)](http://52.20.128.239:3000/)
* [DICOM viewer](https://ivmartel.github.io/dwv/demo/stable/viewers/static/index.html)
* [Ethereum (blockchain)](https://www.ethereum.org/)
* [Tierion (non-repudiation system  - uses blockchain)](https://tierion.com/)
	* <https://tierion.com/proof>
* [IPFS (distributed storage)](https://ipfs.io/). Other alternatives:
  * [MIT Enigma](http://enigma.media.mit.edu/)
  * [Blockstack](https://blockstack.org/)

# FAQ

## What does Tierion do?

Tierion is based on **Proof of Existence**

Use our service to anonymously and securely store an online distributed proof of existence for any document. Your documents are NOT stored in our database or in the bitcoin blockchain, so you don't have to worry about your data being accessed by others.

All we store is a cryptographic digest of the file, linked to the time in which you submitted the document. In this way, you can later certify that the data existed at that time. This is the first online service allowing you to publicly prove that you have certain information without revealing the data or yourself, with a decentralized certification based on the bitcoin network.

The key advantages are anonymity, privacy, and getting a decentralized proof which can't be erased or modified by anyone (third parties or governments). Your document's existence is permanently validated by the blockchain even if this site is compromised or down, so you don't depend or need to trust any central authority. All previous data timestamping solutions lack this freedom.

# Log

### Generate certs for hospitals

* setup DNS for hospitals (mayoclinic.apifocal.org, nashvillecentral.apifocal.org)
* install certbot
* install & configure apache2 (80/443)
* setup vhost for hospital
	* http to https redirect: http://mayoclinic.apifocal.org -> https://mayoclinic.apifocal.org
	* http to https redirect: http://nashvillegeneral.apifocal.org -> https://nashvillegeneral.apifocal.org
* generate certs using letsencrypt

```ssh
sudo ./certbot-auto certonly --webroot -w /var/www/html -d nashvillegeneral.apifocal.org --email alex@apifocal.com
sudo ./certbot-auto certonly --webroot -w /var/www/html -d mayoclinic.apifocal.org --email alex@apifocal.com
```

### Setup a private Ethereum Blockchain

### Create a Smart Contract
