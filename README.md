# Open Plug&Charge Protocol

Here you can find all documents and information about the open source OPCP.

The OPCP protocol is already productivly used since 2019. Many vehicle OEMs, Mobility Operators and Chargepoint Operators are already using this protocol in creating, tranfering, signing ect. of Plug&Charge related infomration based on the standard ISO15118-2 and the VDE Application Guide. 

As it is important to archieve best possible interoperability in the eMobility market it is crucial to use same protocols in the Plug&Charge usecase.

## OPCP enables and reflects following usecases:
  - independent Service Operation
    - [RCP Service](./OPCP-1.0.0/docs/components/01_root-certificate-pool.md)
    - [PCP Service](./OPCP-1.0.0/docs/components/02_provisioning-certificate-pool.md)
    - [CPS Service](./OPCP-1.0.0/docs/components/03_certificate-provisioning-service.md)
    - [CCP Service](./OPCP-1.0.0/docs/components/04_contract-certificate-pool.md)
    - [PKI Authorities](./OPCP-1.0.0/docs/components/05_v2g-pki-services.md)
  - [Authentication Method](./OPCP-1.0.0/docs/04_authentication.md) 
  - [Role specific authentication](./OPCP-1.0.0/docs/04_authentication.md) 
  - Multiple Contracts (EMAIDs) for one Vehicle (PCID)
  - [Standardized Event Service](./OPCP-1.0.0/docs/components/06_webhook-service.md) 
  - Interoperability between Ecosystems, V2G Root Operators etc
    - Multi Root -> CertificateSigningCertificate ability
    - Pool collaboration
  - ISO15118-20 prepared (seperate Namespace already in account)   

## Releases
  - [OPCP 1.0.0](./OPCP-1.0.0/docs/README.md)

## License
[![CC BY-SA 4.0][cc-by-sa-shield]][cc-by-sa]

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0
International License][cc-by-sa].

[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]

[cc-by-sa]: http://creativecommons.org/licenses/by-sa/4.0/
[cc-by-sa-image]: https://licensebuttons.net/l/by-sa/4.0/88x31.png
[cc-by-sa-shield]: https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg
