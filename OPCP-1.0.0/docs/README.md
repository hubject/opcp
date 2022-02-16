# Plug and Charge Ecosystems

**Interface description Version DOC_DATE**

## Introduction

Plug&Charge(PnC) Ecosystems enable EV OEMs, Mobility Operators and Charge Point Operators to use the ISO 15118 standard for the Plug&Charge functionalitie.
PnC-Ecosystems manage certificates from V2G-, OEM- and MO PKIs. It manages the publication in pools  and offers signing services for trusted data. V2G Root CAs like the the Hubject V2G Root CAs are the trust anchor for all participants of ISO 15118. The V2G-, OEM- and MO-CAs are published in the Root Certificate Pools of a Plug&Charge Ecosystem. It is possible to operate also parts like just a RCP, PCP, CPS, CCP or PKI Signing Services

The interfaces of the OPCP are fully compatible with ISO 15118-2: 2014 and the VDE application rule (“VDE Anwendungsregel”). It is also fully interoperable for all relaying parties. The specific implementation/description is based on international best practices, security of communication and protection of data.

The Ecosystem components can be divided into two main categories:
 * The Plug&Charge Certificate pools and Certificate Provisioning Service
 * The Plug&Charge PKI Services
 * The Plug&Charge Callback Service

Plug&Charge PKI Services are managed service of V2G Root Operators like Hubject (Europe & North America), to provide all necessary certificates for EV OEMs, Mobility Operators, Certificate Provisioning Services and Charge Point Operators.

The Certificate pools and Certificate Provisioning Service are for publishing certificates and contracts between all ISO 15118 involved backends.

## Related documents

 * [DIN EN ISO 15118-2:2014: Road vehicles - Vehicle-to-Grid Communication Interface - Part 2: Network and application protocol requirements (ISO 15118-2:2014)](https://www.din.de/en/getting-involved/standards-committees/naautomobil/standards/wdc-beuth:din21:250999944)
 * [VDE Anwendungsregel: VDE-AR-E 2802-100-1, Anwendungsregel: 2017-10, „Zertifikats-Handhabung für E-Fahrzeuge, Ladeinfrastruktur und Backend-Systeme im Rahmen der Nutzung von ISO/IEC 15118“](https://www.vde-verlag.de/normen/0800432/vde-ar-e-2802-100-1-anwendungsregel-2017-10.html)


## Further reading

 * [Business Processes](#business-processes)
 * [Handling of IDs](#handling-of-ids)
 * [Abbreviations](#list-of-abbreviations)


## System-Components

This section describes the components of the Hubject Plug&Charge Ecosystem and their purpose of use.

* [Root Certificate Pool – RCP](#root-certificate-pool) Stores and distributes root certificates of all participating PKIs.
* [Provisioning Certificate Pool – PCP](#provisioning-certificate-pool) stores OEM provisiong certificates and makes them available to the MOs.
* [Certificate Provisioning Service – CPS](#certificate-provisioning-service) provisions contract certificates to prepare them to get installed in the EV.
* [Contract Certificate Pool – CCP](#contract-certificate-pool) stores provisioned contract certificates waiting to get installed.
* [Plug&Charge PKI Services](#pki-services)
* [Plug&Charge Callback/Webhook Service](#webhook-service)
