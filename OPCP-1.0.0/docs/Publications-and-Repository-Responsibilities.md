# Publications and Repository Responsibilities

##	Repositories
In accordance with [VDE-AR](#list-of-abbreviations), the following TLS-protected web-based repositories (except for OSCP and CRL) must be maintained to provide online access via a standard interface to certificates and related data for the participants of the PKI:

### The Root Certificate Pool [RCP](#list-of-abbreviations):
The Root Certificate Pool securely stores V2G-, OEM- and MO Root CA certificates participating in the PKI. Hubject GmbH verifies the authenticity of the root certificate owner before sending a request to the Root Certificate Root responsible (See Chaper *Authentication of organization identity* in the Certificate Policy). Before storing and publishing the root certificates, the following must be checked, and the test results documented and archived:

#### Fingerprint:
The fingerprint must have been authentically obtained via second channel from the corresponding root CA and must correspond to the fingerprint of the certificate. The fingerprints of these Root CA certificates will be published on the Hubject GmbH webpage:
https://www.hubject.com/pki/

#### Revocation:
  The status of the Root certificate shall be confirmed by the owner of the root certificate company.

####	Cryptographic algorithm:
The algorithms used must comply with the ISO 15118 specification. Especially the Certificate Profiles (Annex&nbspF&nbsp\[normative]&nbspCertificate&nbspprofile) must be obeyed.

####	Requirements of ISO 15118
  The certificate structure must comply with the specification in ISO 15118.

#### Certificate Policy: 
- A released, productive and published [CP](#list-of-abbreviations) of the issuing root CA must be available.
-	The requirements in the [CP](#list-of-abbreviations) must guarantee security comparable to the [CP](#list-of-abbreviations) of the Hubject ISO 15118 V2G PKI
-	It must be formally confirmed (by Hubject GmbH or a trusted third party) that the compliance of all requirements has been regulated by a Certificate Practice Statement.

#### Restriction in access
  Write access to the [RCP](#list-of-abbreviations) is restricted to certain employees and IT systems of Hubject GmbH and requires authentication.

####	All activities at the [RCP](#list-of-abbreviations) must be documented and archived.

  -	The same conditions apply for the admission of new/further root certificates as for the initial admission.

  - Naming an usage requirements
  Root certificates that issue subordinate certificates in the respective PKI for test or quality assurance purposes will not be added to the RCP. Successor certificates, i.e. root certificates with the same CN, are neither. Information about the addition of new/further root certificates will be published within a commercially reasonable time (e.g. via Hubject TLS secured website)
  - Random quality checks will be carried out to determine whether a status has changed to a root certificate.
  -	Adding and removing a root certificate to and from the repository are governed by at least a two-man-rule.
  -	A notification channel will be offered which shows changes in the content of the repository and which other subscribers can subscribe to.

### The OEM Provisioning Certificate Pool [PCP](#list-of-abbreviations):
The PCP securely stores the OEM provisioning certificate that is installed individually in each EV an OEM produces. Furthermore, the OEM Provisioning Certificate Pool stores the OEM Sub1-CA certificate and the OEM Sub2-CA certificate to allow signature verification along the OEM certificate chain. All certificates are stored together with the unique OEM provisioning certificate ID (PCID) that is also written in the subject’s common name field of the OEM provisioning certificate. 

###	The Contract Certificate Pool [CCP](#list-of-abbreviations):
The Contract Certificate Pool securely stores pre-compiled contractData which have been signed by the provisioning certificates as described by [VDE_AR](#list-of-abbreviations) and provided by a certificate provisioning service [CPS](#list-of-abbreviations). This data are ready to send in life time as  certificateInstallationResponse message to the OEM or CPO.
