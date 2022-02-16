# Authentication

Your application requires a valid token for calling Hubject APIs. 
This section describes the most important aspects of authentication and authorization for the Hubject PnC EcoSystem. It gets you up and running quickly when working with Hubject APIs. All Endpoints are secured and can only be reached after a successful authentication. 

To establish secure connections via HTTPS, Transport Layer Security (TLS) is used. Hubject requires TLS 1.2 or TLS 1.3 (recommended)

## Oauth2

Hubject is using [OAuth2](https://tools.ietf.org/html/rfc6749) as authentication method. You will need to issue a [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519) that can be obtained by different ways as described in the following sections. The token will contain information about what you are allowed to do, e.g. role (CPO, MO, OEM, CPS), what APIs you are allowed to use and which EMAIDs or PCIDs you are allowed to check.

The issued token will contain all necessary information to access the system (you can check this online on your own e.g. [jwt.io](https://jwt.io/)). 

### Auth0
As Hubject is using [Auth0](https://auth0.com/) to manage the secure access, you as the customer need to issue the token from Auth0 and need to trust the server certificate

[TLS Requirements of Auth0](https://auth0.com/docs/custom-domains/tls-ssl)

## Hubject Server Certs

Hubject is using Server Certificates from Digicert for each stage and world region.

### EU 

QA: 
- DN: `CN=plugncharge-qa.hubject.com,O=Hubject GmbH,L=Berlin,ST=Berlin,C=DE`
- Issuer:`DigiCert Global G2 TLS RSA SHA256 2020 CA1`

Prod: 
- DN: `CN=plugncharge.hubject.com,O=Hubject GmbH,L=Berlin,ST=Berlin,C=DE`
- Issuer:`DigiCert Global G2 TLS RSA SHA256 2020 CA1`

### US

QA: 
- DN: `CN=us.plugncharge-qa.hubject.com,O=Hubject GmbH,L=Berlin,ST=Berlin,C=DE`
- Issuer:`DigiCert Global G2 TLS RSA SHA256 2020 CA1`

Prod: 
- DN: `CN=us.plugncharge.hubject.com,O=Hubject GmbH,L=Berlin,ST=Berlin,C=DE`
- Issuer:`DigiCert Global G2 TLS RSA SHA256 2020 CA1`


### Digicert Root CA
- CommonName: `DigiCert Global G2 TLS RSA SHA256 2020 CA1`
- Issuer: `DigiCert Global Root G2`
- Serial #: `03:3A:F1:E6:A7:11:A9:A0:BB:28:64:B1:1D:09:FA:E5`
- [PEM](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)

### Digicert Intermediate CA
- CommonName: `DigiCert Global G2 TLS RSA SHA256 2020 CA1`
- Issuer: `DigiCert Global Root G2`
- Serial #: `08:5f:94:c0:2d:85:7b:e8:cc:14:ff:53:ed:a2:3e:2a`
- [PEM](https://cacerts.digicert.com/DigiCertGlobalG2TLSRSASHA2562020CA1.crt.pem)

### Digicert Certificate Policy and CertificATE Practise Statement

[Digicert CP](https://content.digicert.com/wp-content/uploads/2020/10/DigiCert-CP-v5.4.1.pdf)

[Digicert CPS](https://content.digicert.com/wp-content/uploads/2020/10/DigiCert-CPS-V.5.4.1.pdf)


## Roles&Rights

Depending on the role and the company the access rights are distinct. 

### OEM
Depending on the WMI in the PCID (first 3 characters), the OEM has read/write access to its data. Please always inform Hubject of the needed WMIs activly. If the correct data are not configured, the Hubject Ecosystem will deny the access to perfom the action.

### MO
Depending on the EMAID (first 5 characters - CountryCode + ProviderID), the MO has read/write access to its data. Please always inform Hubject of the needed Country Codes and ProviderIDs activly. If the correct data are not configured, the Hubject Ecosystem will deny the access to perfom the action.
Reminder: The Hubject Roaming HBS Portal is not connected to the Plug&Charge Ecosystem. No settings are synchronized.

|Service|Access rights                                                                                         |Method                            |Access Rights|OEM      |CPO      |MO with own PKI|Mo with HJ Pki|
|-------|------------------------------------------------------------------------------------------------------|----------------------------------|-------------|---------|---------|---------------|--------------|
|RCP    |OEM, CPO, MO                                                                                          |getRootCert                       |Read         |Access   |Access   |Access         |Access        |
|       |                                                                                                      |getAllRootCerts                   |             |Access   |Access   |Access         |Access        |
|PCP    |OEM (Only those with the corresponding WMI), (MO is allowed to get all PCIDs)|addOemProvCert                    |Write        |Access   |No Access|No Access      |No Access     |
|       |                                                                                                      |deleteOemProvCert                 |Delete       |Access   |No Access|No Access      |No Access     |
|       |                                                                                                      |getOEMProvCert                    |Read         |Access   |No Access|Access         |Access        |
|       |                                                                                                      |lookupVehicle                     |Read         |Access   |No Access|Access         |Access        |
|CPS    |MO with own PKI (external PKI) (only their own EMAIDS)                                                |createSignedContractData          |(Read)       |No Access|No Access|Access         |No Access     |
|       |                                                                                                      |createAndForwardSignedContractData|Write        |No Access|No Access|Access         |No Access     |
|       |MO without own PKI (Hubject PKI) (only their own EMAIDS)                                              |generateSignedContractData        |Write        |No Access|No Access|No Access      |Access        |
|CCP    |CPO                                                                                                   |getSignedContractData             |Read         |No Access|Access   |No Access      |No Access     |
|       |MO                                                                                                    |deleteSignedContractData          |Delete       |No Access|No Access|Access         |Access        |
|       |MO                                                                                                    |lookupContract                    |Read         |No Access|No Access|Access         |Access        |
|       |OEM                                                                                                   |provideSignedContractData         |Read         |Access   |No Access|No Access      |No Access     |
|       |OEM                                                                                                   |signedContractData                |Read         |Access   |No Access|No Access      |No Access     |
|       |OEM                                                                                                   |signedContractData/priorities     |Read         |Access   |No Access|No Access      |No Access     |
|EST    |OEM (usage should be counted by OEM-user)                                                             |simpleEnroll - OEM                |Read & Write |Access   |No Access|No Access      |No Access     |
|       |                                                                                                      |caCerts - OEM                     |Read         |Access   |No Access|No Access      |No Access     |
|       |CPO (usage should be counted by CPO-user)                                                             |simpleEnroll - CPO                |Read & Write |No Access|Access   |No Access      |No Access     |
|       |                                                                                                      |caCerts - CPO                     |Read         |No Access|Access   |No Access      |No Access     |
|       |MO (usage should be counted by MO-user)                                                               |simpleEnroll - MO                 |Read & Write |No Access|No Access|No Access      |Access        |
|       |                                                                                                      |caCerts - MO                      |Read         |No Access|No Access|No Access      |Access        |


