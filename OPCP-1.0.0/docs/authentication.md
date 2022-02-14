# Authentication

This section describes the most important aspects of authentication and authorization for an PnC EcoSystem. All Endpoints shall be secured and can only be reached after a successful authentication. 

To establish secure connections via HTTPS, Transport Layer Security via TLS 1.3 is recommended.

## Oauth2

It is recommended in using [OAuth2](https://tools.ietf.org/html/rfc6749)as authentication method. You will need to issue a [JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519) that can be obtained by different ways as described in the following sections. The token will contain information about what you are allowed to do, e.g. role (CPO, MO, OEM, CPS), what APIs you are allowed to use and which EMAIDs or PCIDs you are allowed to check.

The issued token will contain all necessary information to access the system (you can check this online on your own e.g. [jwt.io](https://jwt.io/)). 

## Roles&Rights

Depending on the role and the company the access rights are distinct. 

### OEM
Depending on the WMI in the PCID (first 3 characters), the OEM has read/write access to its data. Please always inform the ecosystem operator of the needed WMIs activly. If the correct data are not configured, the Plug&Charge Ecosystem will deny the access to perfom the action.

### MO
Depending on the EMAID (first 5 characters - CountryCode + ProviderID), the MO has read/write access to its data. Please always inform the ecosystem operator of the needed Country Codes and ProviderIDs activly. If the correct data are not configured, the Plug&Charge Ecosystem will deny the access to perfom the action.

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


