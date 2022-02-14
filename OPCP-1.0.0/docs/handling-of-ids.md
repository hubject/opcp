

# Handling of IDs

## EMAID (E-Mobility Authentication Identifier)

EMAIDs in the definition of ISO-15118 have some representational flexibility due to optional elements. The Hubject Plug and Charge ecosystem will therefore normalize all incoming IDs to match the following expression: `/[A-Z]{2}[\dA-Z]{3}[\dA-Z]{9}/i`
However the version with optional seperators (“-”) and check digit is allowed : `/[a-z]{2}(-?)[\da-z]{3}\1[\da-z]{9}(\1[\da-z])?/i`. Nevertheless the Hubject ecosystem will always remove Hyphens from the EMAID due to the ISO15118-2 Protocol, where just max. 15 characters can be transfered between EV and EVSE.

ABNF from the ISO 15118-2:2014(E):

`<EMAID>` = `<Country Code>` `<S>` `<Provider ID>` `<S>` `<eMA Instance>` `<S>` `<Check Digit>`

Clients can still use it but the system will normalize to the form above (no seperators and captial letters).

## PCID (Provisioning Certificate Identifier)

PCIDs in the definition of ISO-15118 are represented by the WMI (3 Characters) of the OEM, followed by 14 alphanumeric characters which uniqly identifies the vehicle and an optional check digit/alpha. The Hubject Plug and Charge ecosystem check all incoming IDs to match the following expression: `^[a-zA-Z0-9]{17,18}$`

ABNF from VDE-AR-E 2802-100-1:2019-12 (en)
`<PCID>` = `<WMI>` `<OEM's own unique ID>` `<check digit>`

## EVSE ID (Electric Vehicle Supply Equipment ID)

The EVSEID shall match the following structure (the notation corresponds to the augmented Backus-Naur Form (ABNF) as defined in IETF RFC 5234):

ABNF from the ISO 15118-2:2014(E):

`<EVSEID>` = `<Country Code>` `<S>` `<EVSE Operator ID>` `<S>` `<ID Type>` `<Power Outlet ID>`

An example for a valid EVSEID is `DE*ICE*E45B*78C` with `DE` indicating Germany, `ICE` representing Hubjects EVSE Operator ID, `E` indicating that it is of type *EVSE*, `45B` representing the number of this EVSE and `78C` representing one particular power outlet of this specific EVSE.