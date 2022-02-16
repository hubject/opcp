# Business Processes

THis section summarizes all processes of Plug and Charge as described as _Certificate Provisioning_ in ISO 15118 Section 7.9.2.5 and explained in more detail in Appendix E.3.

The VDE Application Rule focusses on these processes and details each process flow for further understanding. The following figure shows the overall process with components and flows, which are based on the VDE Application Rule.

![Overview on the overall process](../assets/images/process_overview.png)

During contract provisioning, several sub-processes are also required, which can be divided into four main parts:

 1. **Vehicle production and preparation of contract based billing**
   - The OEM generates a Provisioning Certificate for each electric vehicle during production.
   - The OEM installs a trust store containing all relevant Root Certificates from the Root Certificate Pool.
 2. **Contract conclusion and vehicle assignment**
   - The MO concludes a charging contract for a specific customer's electric vehicle, using the vehicles Provisioning Certificate from the Provisioning Certificate Pool.
   - Providing contract data to the Certificate Provisioning Service or
   - Providing contract information to V2G Mobility Operator CA
  3. **(Periodic) provisioning of contract data**
   - Signing contract data and storing in the CCP
   - Generating contract data in V2G Mobility Operator CA and storing in the CCP
 4. **Installation of contract data**
   - Providing signed contract data to CPO-backend on request
   - Delivery of signed contract data to OEM-backend


## Business Processes relevant for all participants

#### Providing Root Certificates for Public Charging and Contract-Based Billing
The mutual trust between participants is a precondition for ISO 15118 and thus Plug&Charge to function. For this purpose, a Root Certificate Pool is set up for the storage of all Root certificates. Each participant gets access to receive the Root certificates of other participants to validate the trust chain of each certificate.

![Providing root certificates for public charging and contract-based billing](../assets/images/process_providing_root_certificates.png)



## Business Processes relevant for the CPO

### Providing Signed Contract Data to CPO-Backend on Request

Alternative to the OEM backend, is the installation of signed contract data via the charging station. The OEMs, which do not use an OEM backend, can use this process for the delivery of contract data.
After a successful handshake between EV and charging device, the EV sends a certificateInstallationRequest to the charging device, which will be forwarded via the CPO backend to the CCP.
The CCP finds the contracts of this EV, verifies the validity of each certificate and delivers it back to the CPO backend.

![Providing signed contract data to CPO backend on request](../assets/images/process_providing_signed_contract_data_to_cpo_backend_on_request.png)


## Business Processes relevant for the MO

### Contract Conclusion and Vehicle Assignment

This process describes, the conclusion of contract between customer and MO and delivery of OEM provisioning certificate of vehicle to the MO.
The MO must receive the contract information from a customer including the PCID of the vehicle. The PCID must be sent by the MO to the PCP. The PCP delivers the OEM provisioning certificate, including the corresponding Sub CA chain (See Figure 5).

![Conclusion of contract and receiving vehicle certificate from vehicle Certificate Pool](../assets/images/process_conclusion_of_contract_and_receiving_vehicle_certificate_from_pcp.png)

After verifying the authenticity of the trust chain with the OEM root certificate (which has been received from the Root Certificate Pool), the MO can generate a unique e-mobility account identifier for this contract. To create a contract for the customer, MOs have two possibilities:

 - Create and send the contract data to the CPS using the MOs own CA, which is described in the “Providing Contract Data to Certificate Provisioning Service” process;
 - Or use V2G-PKI MO CA services to create, sign and store the contract data


### Providing Contract Data to Certificate Provisioning Service

If the MO uses its own CA, it must create a contract data with the following parts:
 - contractSignatureCertChain,
 - dhPublicKey,
 - contractSignatureEncryptedPrivateKey,
 - EMAID

The created contract data must be signed by the CPS.

Moving forward, MOs have two possibilities:
 - Using createAndForwardSignedContratData interface for signing and storing of signed contract data in the CCP;
 - Or sending the contract data with createSignedContractData interface of OPCP to receive the signed contract data back after the signing by the CPS.


<!-- ![Providing contract data to certificate Provisioning Service](../assets/images/process_providing_contract_data_to_certificate_provisioning_service.png) -->


### Providing Contract Information to V2G-PKI Mobility Operator CA

In this process, MOs would not use the createSignedContractData interface. CPS Operator would do this based on the generateSignedContractData interface. After receiving a PCID from the customer and generating an EMAID, the MO sends the contract information to the V2G Mobility Operator CA to create a contract data. The contract information includes PCID, EMAID and contracts begin and end dates.

![Providing contract information to V2G Mobility Operator CA](../assets/images/process_providing_contract_information_to_hubject_mobility_operator_ca.png)


### Periodic Provisioning of Contract Data

Signing Contract Data and Storing in CCP
The CPS signs the delivered contract data with the V2G Root CA derived private key. Then the CPS either stores it in the CCP for provisioning for the CPO and OEM backends or sends it back to the MO.
In this latter method, the MO would have to use addSignedContractData to store contract data in the CCP. For the procedural differences, please refer to chapter Fehler: Verweis nicht gefunden.

![Signing contract data and storing in CCP](../assets/images/process_signing_contract_data_and_storing_in_ccp.png)


### Generating Contract Data with CPS Mobility Operator CA and Storing in CCP

If the MO does not create and sign the contract data (using createSignedContractData method), the COS Operator Mobility Operator CA can generate a contract data with the received contract information from the MO. The CPS Operator would then send the contract data to the CPS for signing and then store the signed contract data in the CCP.

![Generating contract data with the CPS Mobility Operator CA service and storing in CCP](../assets/images/process_generating_contract_data_in_hubject_mo_ca.png)




## Business Processes relevant for the OEM

### Production of Vehicles and Storing Provisioning Certificate

With the production of the vehicle, the OEM must create a provisioning certificate for each vehicle with a unique provisioning certificate identifier – PCID. The OEM sends this unique OEM provisioning certificate corresponding subordinate CA (Sub CA) certificates securely to the Provisioning Certificate Pool.
The customers shall also receive the PCID of their vehicles to give it to the MOs, during the conclusion of a charging contract.
The required V2G root certificates shall also be installed and stored in the vehicle for the trusted communication with charging devices and to verify contract data.

![Production of vehicles and storing provisioning certificate](../assets/images/process_production_of_vehicles_and_storing_provisioning_certificate.png)


### Installation of Contract Data

See [Providing Signed Contract Data to CPO-Backend on Request](#providing-signed-contract-data-to-cpo-backend-on-request) from the CPO processes.

## Pool management

 * Revoking a certificate removes it in regular checks from pools.
 * Expired certificates will also be removed by regular batch jobs
 * Cleanup of CCP if the regarding Prov Cert got removed from the PCP
