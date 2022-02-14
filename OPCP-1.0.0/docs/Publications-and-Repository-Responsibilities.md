# Publications and Repository Responsibilities

##	Repositories
In accordance with [VDE-AR](#list-of-abbreviations), the following repositories (except for OSCP and CRL) must be maintained to provide online access via a standard interface to certificates and related data for the participants of the ecosystem.

### The Root Certificate Pool [RCP](#list-of-abbreviations):
The Root Certificate Pool securely stores V2G-, OEM- and MO Root CA certificates participating in the PKI. The RCP operator verifies the authenticity of the root certificate owner before stroring them into the Root Certificate Root.

#### Fingerprint:
The fingerprint must have been authentically obtained via second channel from the corresponding root CA and must correspond to the fingerprint of the certificate.

#### Revocation:
The status of the Root certificate shall be confirmed by the owner of the root certificate company.

####	Requirements of ISO 15118
The certificate structure must comply with the specification in ISO 15118.

#### Restriction in access
Write access to the [RCP](#list-of-abbreviations) is restricted to certain employees and IT systems of RCP operator and requires authentication.

####	All activities at the [RCP](#list-of-abbreviations) shall be documented and archived.

### The OEM Provisioning Certificate Pool [PCP](#list-of-abbreviations):
The PCP securely stores the OEM provisioning certificate that is installed individually in each EV an OEM produces. Furthermore, the OEM Provisioning Certificate Pool stores the OEM Sub1-CA certificate and the OEM Sub2-CA certificate to allow signature verification along the OEM certificate chain. All certificates are stored together with the unique OEM provisioning certificate ID (PCID) that is also written in the subject’s common name field of the OEM provisioning certificate. 

###	The Contract Certificate Pool [CCP](#list-of-abbreviations):
The Contract Certificate Pool securely stores pre-compiled contractData which have been signed by the provisioning certificates as described by [VDE_AR](#list-of-abbreviations) and provided by a certificate provisioning service [CPS](#list-of-abbreviations). This data are ready to send in life time as certificateInstallationResponse message to the OEM or CPO.
