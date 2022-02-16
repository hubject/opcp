# Certificate Provisioning Service

The CPS provides interfaces for generating and signing contract data of MOs. MOs can provide a contract data to sign in CPS or send contract information to generate contract data in the Hubject Mobility Operator CA. The signed contract data are either returned to the MO or stored in the CCP.


## API

The Certificate Provisioning Service can receive and sign a contract data through a REST API, using one of the two availables endpoints: 

- CreateSignedContractData: receive, signs and returns a signed contract data.
- CreateAndForwardSignedContractData: receive, signs a contract data, and forwards to the Certificate Pool.

![CCP interfaces](../../assets/images/interfaces_cps.png)

All CCP API documenatation can be found at `cps.v1.yaml`.

