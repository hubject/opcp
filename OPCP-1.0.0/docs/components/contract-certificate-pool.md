# Contract Certificate Pool

The CCP stores the signed contract data of the MOs and provides it to the CPO and OEM backend. The CPO backend can request signed contract data in the form of certificateIntallationRequest, which is defined in ISO 15118-2:2014. It also provides signed contract data to the OEM backend.

The by the CPS signed contract data will be stored in CCP and assigned to their respective PCID. In the CCP, it is possible to store multiple contracts for each car.

The CCP keeps contracts of each MO separate. The defined access rules prevent access to other MO contracts. Each MO can manage (create/update/delete) only contracts of their own company.

The Hubject administration creates a node for each MO after the confirmation of provider ID by the issuing authority.


## API

The Contract Certificate Pool offers a REST API to request registered Provisioning Certificates.

All CCP API documenatation can be found at `ccp.v1.yaml`.

## Data Cleansing
         
The Contract Certificate Pool shall be cleaned up on regular basis.
