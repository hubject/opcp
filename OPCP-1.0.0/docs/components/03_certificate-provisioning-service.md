# Certificate Provisioning Service

The CPS provides interfaces for generating and signing contract data of MOs. MOs can provide a contract data to sign in CPS or send contract information to generate contract data via the V2G-Operator Mobility Operator CA. The signed contract data are either returned to the MO or stored in the CCP.


## API

The Certificate Provisioning Service can receive and sign contract data through a REST API, using one of the multiple endpoints. The signed data can be optionaly stored into Contract Certificate Pool (this is usualy the case).

![CPS interfaces](../../assets/images/interfaces_cps.png)

All CPS API documenatation can be found at [cps.v1.json](./../../reference/cps.v1.json).

