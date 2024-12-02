# 3535 Recommendations Status Check

## Summary

| RFC3535 Recommendation Label           | Status                                                                                                 | 
|---------------------------------------:|:-------------------------------------------------------------------------------------------------------|
| 3535-RECO-STOP-MANDATE-MIB             | Done, IESG Statement on Writable MIB Module (2014)                                                     |
| 3535-RECO-MIB-INVESTIGATE              | No such group was formed                                                                               |
| 3535-RECO-SNMP-WG4MONITORING           | No such group was formed                                                                               |
| 3535-RECO-FOCUS-IETF-CONFIG-MECHANISMS | NETCONF/RESTCONF/CORECONF/YANG/COMI/etc.                                                               |
| 3535-RECO-FOCUS-XML                    | OK                                                                                                     |
| 3535-RECO-NO-HTTP                      | The IETF deviated from this recommendation, e.g., RESTCONF or CoAP Management Interface (CORECONF)     |
| 3535-RECO-MAINTAIN-SMI-SPPI            | SMIng WG was concluded in 2003-04-04                                                                   |
| 3535-RECO-IETF2FIX-MIB                 | The IETF dedicated resources to fix some SNMP shortcomings with a focus on security                    |
| 3535-MISC-NO-CIM                       | The IETF didn't dedicate any resources on CIM extensions                                               |
| 3535-MISC-ABANDON-COPS-PR              | OK. The IETF has reclassified COPS-PR to Historic status                                               |
| 3535-MISC-ABANDON-PIB                  | OK. The IETF has reclassified SPPI, as well as three PIBs to Historic status                           |

## Detailed

# Assessment of RFC 3535 Recommendations

>      (3535-RECO-STOP-MANDATE-MIB) The workshop recommended that the IETF stop forcing working groups
>      to provide writable MIB modules.  It should be the decision of
>      the working group whether they want to provide writable objects
>      or not.

**Status Update**:
: In 2014, the IESG published a [statement on Writable MIB Module](https://datatracker.ietf.org/doc/statement-iesg-writable-mib-module-iesg-statement-20140302/), which states that:

   > SNMP MIB modules creating and modifying configuration state should only be produced by working groups in cases of clear utility and consensus to use SNMP
 write operations for configuration, and in consultation with the OPS ADs/MIB doctors.

>      (3535-RECO-MIB-INVESTIGATE) The workshop recommended that a group be formed to investigate why
>      current MIB modules do not contain all the objects needed by
>      operators to monitor their networks.

**Status Update**:
: No such group was formed to our knowledge.


>      (3535-RECO-SNMP-WG4MONITORING) The workshop recommended that a group be formed to investigate why
>      the current SNMP protocol does not satisfy all the monitoring
>      requirements of operators.

**Status Update**:
: No such group was formed to our knowledge.

>      (3535-RECO-FOCUS-IETF-CONFIG-MECHANISMS) The workshop recommended, with strong consensus from both protocol
>      developers and operators, that the IETF focus resources on the
>      standardization of configuration management mechanisms.

**Status Update**:
: NETCONF ([RFC6241](https://datatracker.ietf.org/doc/html/rfc6241)), RESTCONF ([RFC8040](https://datatracker.ietf.org/doc/html/rfc8040)), CORECONF ([I-D.ietf-core-comi](https://datatracker.ietf.org/doc/draft-ietf-core-comi/)), YANG.
: YANG is a transport-independent data modeling language. It can be used independently of NETCONF/RESTCONF.
For example, YANG can be used to define abstract data structures ([RFC8791](https://datatracker.ietf.org/doc/html/rfc8791)) that can be manipulated by other protocols (e.g., ([RFC9132](https://datatracker.ietf.org/doc/html/rfc9132))).

>      (3535-RECO-FOCUS-XML) The workshop recommended, with strong consensus from the operators
>      and rough consensus from the protocol developers, that the
>      IETF/IRTF should spend resources on the development and
>      standardization of XML-based device configuration and management
>      technologies (such as common XML configuration schemas, exchange
>      protocols and so on).

**Status Update**:
: OK. This recommendation was also mirrored in other documents such as [RFC5706](https://datatracker.ietf.org/doc/html/rfc5706).

>      (3535-RECO-NO-HTTP) The workshop recommended, with strong consensus from the operators
>      and rough consensus from the protocol developers, that the
>      IETF/IRTF should not spend resources on developing HTML-based or
>      HTTP-based methods for configuration management.

 **Status Update**:
 : The IETF deviated from this recommendation, e.g., RESTCONF ([RFC8040](https://datatracker.ietf.org/doc/html/rfc8040)) or CoAP Management Interface (CORECONF) ([I-D.ietf-core-comi](https://datatracker.ietf.org/doc/draft-ietf-core-comi/)).

>      (3535-RECO-MAINTAIN-SMI-SPPI) The workshop recommended, with rough consensus from the operators
>      and strong consensus from the protocol developers, that the IETF
>      should continue to spend resources on the evolution of the
>      SMI/SPPI data definition languages as being done in the SMIng
>      working group.

**Status Update**:
: SMIng WG was concluded in 2003-04-04.

>      (3535-RECO-IETF2FIX-MIB) The workshop recommended, with split consensus from the operators
>      and rough consensus from the protocol developers, that the IETF
>      should spend resources on fixing the MIB development and
>      standardization processs.

**Status Update**:
: The IETF dedicated some resources to fix some SNMP shortcomings with a focus on security (e.g., Transport Layer Security
(TLS) Transport Model for the SNMP ([RFC6353](https://datatracker.ietf.org/doc/html/rfc6353)) or ([RFC9456](https://datatracker.ietf.org/doc/html/rfc9456)), HMAC-SHA-2 Authentication Protocols in User-Based Security Model (USM) for SNMPv3 ([RFC7860](https://datatracker.ietf.org/doc/html/rfc7860))).

[Section 6 of RFC3535](https://datatracker.ietf.org/doc/html/rfc3535#autoid-12) also includes the following but without tagging them as recommendations:

>      (3535-MISC-NO-CIM) The workshop had split consensus from the operators and rough
>      consensus from the protocol developers, that the IETF should not
>      focus resources on CIM extensions.

**Status Update**:
: The IETF didn't dedicate any resources on CIM extensions.

>      (3535-MISC-ABANDON-COPS-PR) The workshop had rough consensus from the protocol developers
>      that the IETF should not spend resources on COPS-PR development.
>      So far, the operators have only very limited experience with
>      COPS-PR.  In general, however, they felt that further development
>      of COPS-PR might be a waste of resources as they assume that
>      COPS-PR does not really address their requirements.

**Status Update**:
: The IETF has reclassified COPS Usage for Policy Provisioning ([RFC3084](https://datatracker.ietf.org/doc/html/rfc3084))
  to Historic status.

>      (3535-MISC-ABANDON-PIB) The workshop had rough consensus from the protocol developers
>      that the IETF should not spend resources on SPPI PIB definitions.
>      The operators had rough consensus that they do not care about
>      SPPI PIBs.

**Status Update**:
: The IETF has reclassified Structure of Policy Provisioning Information ([RFC3159](https://datatracker.ietf.org/doc/html/rfc3159)), as well as
  three Policy Information Bases ([RFC3317](https://datatracker.ietf.org/doc/html/rfc3317), [RFC3318](https://datatracker.ietf.org/doc/html/rfc3318), and [RFC3571](https://datatracker.ietf.org/doc/html/rfc3571)) to Historic status.
