---
title: "RFC 3535,  20 Years Later: An Update of Operators Requirements on Network Management Protocols and Modelling"
abbrev: "RFC 3535, 20 Years Later"
category: info

docname: draft-boucadair-nmop-rfc3535-20years-later-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
# area: OPS
# workgroup: WG Working Group
keyword:
 - network management
 - future networks

author:
 -
   fullname: Mohamed Boucadair
   organization: Orange
   email: mohamed.boucadair@orange.com
 -
   fullname: Luis Miguel Contreras Murillo
   organization: Telefonica
   email: luismiguel.contrerasmurillo@telefonica.com
 -
   fullname: Oscar Gonzalez de Dios
   organization: Telefonica
   email: oscar.gonzalezdedios@telefonica.co
 -
   fullname: Thomas Graf
   organization: Swisscom
   email: thomas.graf@swisscom.com

normative:

informative:


--- abstract

The IAB has organized an important workshop
to establish a dialog between network operators and
protocol developers, and to guide the IETF focus on work
regarding network management.  The outcome of that workshop
was documented in the "IAB Network Management Workshop" (RFC 3535)
which was instrumental for developing NETCONF and YANG, in particular.

20 years later, it is time to evaluate what has been achieved since then and
identify the operational barriers for making these
technologies widely implemented. Also, this document intends to capture new
requirements for network management operations.

--- middle

# Introduction

The IAB has organized a workshop (June 4-June 6, 2002)
to establish a dialog between network operators and
protocol developers, and to guide the IETF focus on work
regarding network management.  The outcome of that workshop
was documented in the "IAB Network Management Workshop" {{?RFC3535}}
which was instrumental for developing NETCONF {{?RFC6241}}, YANG {{?RFC6020}}{{?RFC7950}}, and RESTCONF {{?RFC8040}}.

20 years later, new requirements on network management operations are emerging from the operators. This document intends to capture these requirements that reflect the progress in this area. The document also provide an assessment of the RFC3535 recommendations and to what extend that roadmap was driving network management efforts within the IETF.

Early version of the document includes **many placeholders on purpose** as the intent is to collect inputs from interested parties. Items listed in {{sec-obs}} are provided to exemplify candidate items to discuss in that section.

# Summary of Technology Advences Since RFC 3535

To be further elaborated:

* NETCONF
* YANG
* RESTCONF
* SDN & Programmable Networks
* Automation
* Virtualization
* Containerization
* Intent-based
* Network APIs
* Telemetry

See also "An Overview of the IETF Network Management Standards" {{?RFC6632}}.

# Assessment of RFC 3535 Recommendations

{{Section 6 of ?RFC3535}} includes the following recommendations:

   1.  The workshop recommends that the IETF stop forcing working groups
       to provide writable MIB modules.  It should be the decision of
       the working group whether they want to provide writable objects
       or not.

       **Status Update**: In 2014, the IESG published a statement Writable MIB Module, which states that:
         > SNMP MIB modules creating and modifying configuration state should only be produced by working groups in cases of clear utility and consensus to use SNMP
 write operations for configuration, and in consultation with the OPS ADs/MIB doctors.

   3.  The workshop recommends that a group be formed to investigate why
       current MIB modules do not contain all the objects needed by
       operators to monitor their networks.

       **Status Update**: xxx

   4.  The workshop recommends that a group be formed to investigate why
       the current SNMP protocol does not satisfy all the monitoring
       requirements of operators.

       **Status Update**: xxx

   5.  The workshop recommends, with strong consensus from both protocol
       developers and operators, that the IETF focus resources on the
       standardization of configuration management mechanisms.

       **Status Update**: NETCONF, RESTCONF, CORECONF, YANG.

   6.  The workshop recommends, with strong consensus from the operators
       and rough consensus from the protocol developers, that the
       IETF/IRTF should spend resources on the development and
       standardization of XML-based device configuration and management
       technologies (such as common XML configuration schemas, exchange
       protocols and so on).

       **Status Update**: OK. This recommendation was also mirrored in other documents such as {{?RFC5706}}.

   7.  The workshop recommends, with strong consensus from the operators
       and rough consensus from the protocol developers, that the
       IETF/IRTF should not spend resources on developing HTML-based or
       HTTP-based methods for configuration management.

       **Status Update**: The IETF deviated from this recommendation, e.g., RESTCONF {{?RFC8040}} or CoAP Management Interface (CORECONF) {{?I-D.ietf-core-comi}}.

   8.  The workshop recommends, with rough consensus from the operators
       and strong consensus from the protocol developers, that the IETF
       should continue to spend resources on the evolution of the
       SMI/SPPI data definition languages as being done in the SMIng
       working group.

       **Status Update**: SMIng WG was concluded in 2003-04-04.

   9.  The workshop recommends, with split consensus from the operators
       and rough consensus from the protocol developers, that the IETF
       should spend resources on fixing the MIB development and
       standardization processs.

       **Status Update**: The IETF dedicated some resources to fix some
       SNMP shortcomings with a focus on security (e.g., Transport Layer Security (TLS) Transport Model for
       the SNMP {{?RFC6353}} or {{?RFC9456}}, HMAC-SHA-2 Authentication Protocols in User-Based Security Model (USM) for SNMPv3 {{?RFC7860}}).

{{Section 6 of ?RFC3535}} also includes the following but without tagging them as recommendations:

   1.  The workshop had split consensus from the operators and rough
       consensus from the protocol developers, that the IETF should not
       focus resources on CIM extensions.

       **Status Update**: The IETF didn't dedicate any resources on CIM extensions.

   2.  The workshop had rough consensus from the protocol developers
       that the IETF should not spend resources on COPS-PR development.
       So far, the operators have only very limited experience with
       COPS-PR.  In general, however, they felt that further development
       of COPS-PR might be a waste of resources as they assume that
       COPS-PR does not really address their requirements.

       **Status Update**: The IETF has reclassified COPS Usage for Policy Provisioning {{?RFC3084}}
       to Historic status.

   3.  The workshop had rough consensus from the protocol developers
       that the IETF should not spend resources on SPPI PIB definitions.
       The operators had rough consensus that they do not care about
       SPPI PIBs.

       **Status Update**: The IETF has reclassified Structure of Policy Provisioning Information {{?RFC3159}}, as well as
       three Policy Information Bases ({{?RFC3317}}, {{?RFC3318}}, and {{?RFC3571}}) to
       Historic status.

# Some Observations {#sec-obs}

## Fragmented Ecosystem

The current YANG device models ecosystem is **fragmented**: some
standards models are defined in the IETF while similar ones are
defined in other fora such as Openconfig or ONF. Unlike service and
network models, IETF-defined device models are not widely
implemented. There is a need to rationalize this space and
avoid redundant efforts.

## Lack of Profiling

Many NETCONF-related tools are (being) specified by the IETF,
but these tools are not widely supported (e.g., Push). Editing a
profile document with a set of recommendations about core/key
features with the appropriate justification will help the
emergence of more implementations that meet the operators’
needs.

> Examples of such profile documents are the various RFCs that were published by the behave WG {{?BCP127}}.
> Another approach is to consider an appraoch similar to the "Roadmap for Transmission Control Protocol (TCP) Specification Documents" {{?RFC7414}}. Such a document
> would serve as a guide and reference for implementers and any other parties who desire information contained in the 'NETCONF/RESTCONF/YANG'-related RFCs.

Likewise, reassess the value of some IETF proposals vs. competing/emerging solutions would be useful (e.g., gRPC vs. YANG-Push).

## Lack of Agile Process for (The Maintenance of) YANG Modules

RFCs might not be suited for documenting YANG modules. In the meantime, there is a need for
"reference models" and "sufficiently stable models". An
hybrid approach might be investigated for documenting IETF-
endorsed YANG modules, such as considering an RFC to
describe the initial module sketch and objectives and an
official IETF repository for maintaining intermediate YANG
versions.

## Integration Complexity (Thomas)

Section 3 of RFC 3535 describes the network operator requirements. One of the requirements describe the ease of use which according to RFC 6244 section 3.2 is addressed by Netconf and YANG. For configuration this holds true, for network observability unfortunately not yet. This has been confirmed with a set of network operators by asking how long it takes from subscribing YANG data to make it accessible to the operator. Minutes, Hours, Days or Weeks. None of them answered Minutes or Hours. All of them responded Days or Weeks. Hinting manual post processing of YANG data.

Collecting YANG metrics from networks is already a struggle due to late arrival of RFC 8639, RFC 8640 and RFC 8641 and draft-ietf-netconf-https-notif and draft-ietf-netconf-udp-notif for configured subscription transport protocols which defined YANG-Push in the industry. This caused network vendors to implement alternative ways to collect real-time streaming data in the meanwhile, such as gNMI which was proposed in 2018 draft-openconfig-rtgwg-gnmi-spec to the IETF but not followed up on. Unfortunately, these implementations differ between network operating systems due to the lack of standardization, specifically for the metadata which would ensure machine readability.

When a set of network operators where asked to where operational YANG data needs to be integrated to, the answer homogeneously was Apache Kafka Message Broker and Time Series Databases. draft-netana-nmop-yang-kafka-integration defines an architetcture how YANG-Push can be integrated into Apache Kafka and references needed YANG-Push extensions and defines requirements for YANG schema registry development. The YANG-Push extensions addressing needs to make YANG-Push messages machine readable and against semantic validate able to ensure a consistent data processing. One of the current challenges is that the subscribed YANG data referenced with datastore-subtree-filter or datastore-xpath-filter breaks semantic integrity which needs to be addressed by either updating Section 4 of RFC 8641 or proposing a new YANG module being used at the YANG-Push receiver as described in Section 5 of draft-netana-nmop-yang-kafka-integration.

## YANG-formatted Data Manipulation

TBC.

## Translation and Mapping Between Service/Network and Device Models (Oscar)

TBC.

## (In)Consistent Data Structures in Network Protocols for Data Export (Thomas)

Network Telemetry as described in RFC 9232 are a set of protocols. Due to the different requirements, one Network Telemetry protocol doesn't address all needs. This is mainly due to the nature of the subscribed data. BMP as defined in RFC 7854 adds monitoring and tracing capabilities natively to the BGP process to minimize the processing overhead. While IPFIX as defined in RFC 7011 and RFC 7012 can be applied according to RFC 5472 to gain visibility into the data and forwarding plane, due to the amount of data, sampling as defined in RFC 5476 and applied to IPFIX in RFC 5477 and aggregation as defined in RFC 7015 for IPFIX is needed to reduce the amount of exposed data. While YANG-Push focuses on exposing already YANG modelled data, which eases the correlation among network configuration and operational data.

RFC 9232 is an informational document and does not specify what these Network Telemetry protocols should have in common to ensure consistent data structures for data export. While data types are fairly good aligned, a lack of metadata standardization among the Network Telemetry protocols is observed. In particular describing from where the metrics has been exported from and timestamping. draft-tgraf-netconf-notif-sequencing and draft-netconf-yang-push-observation-time addresses this for YANG-Push. In section 4.2 of RFC 7854 timestamps are optional and sysName, RC 1213, is only carried in the BMP initiation message described in section 4.3. While the message header of IPFIX defined in section 3.1 lacks the sysName definition.

The lack of information from where the data is being pushed from is only known to the Network Telemetry data collection due to the transport session being established from the network node exporting the information. When Network Telemetry messages are being transformed and forwarded, this information is being lost. Therefore, it is common among network operators to augment sysName and other metadata, example draft-claise-opsawg-collected-data-manifest at the data collection.

The same common principle applies to when observation timestamping is missing in the Network Telemetry message. Since the data collection is the closest element to the network, a time stamp is added to give the network operator at least the information when the Network Telemetry message was collected. However, since Network Telemetry addresses real-time streaming needs, this is often not accurate enough for data correlation.

## Proprietary YANG Modules, CLI, and Limited Abstraction (Oscar)

Pluggins/Proxy YANG/CLI is still the rule in many operations.

Complexity in dev the pluggins (as you need to cover many OS/vendors).

Network models for the realization provides some "level" of abstraction and then automations.

TBC.

## Distinct Networks, Distinct Management Requirements

From the time RFC 3535 was released up to now, new kind of services and applications have been developed and deployed over the time, with very diverse, and some times contradicting, requirements. Those services have been engineered on top of multi-service networks for the sake of efficiency and simplicity, accommodating such a variety of needs. As a result, services requiring mobility, data replication, large capacity, adaptability, multi-path support, determinism, etc., coexist on the same shared network, needing from it mechanisms for graceful operation.

Likewise, such diversity of services also require different management capabilities. For example, session continuity, distribution trees, traffic engineering, congestion status notification, reordering, or on-time delivery impose very different management needs to be satisfied.

This reality is different from the one existing at the time of {{?RFC3535}}, and as such, the new identified needs can require from novel approaches to guarantee the aforementioned co-existence of services.

Also, some networks have specific network management requirements such as the need for asynchronous operations or constraints on data compactness. An example of such networks is Delay-Tolerant Networking (DTN) {{?RFC838}}.

## Implications of External Dependency

Networks are being updated to abandon the silo approach from the past towards an increasing convergence. Specifically, there are trends towards a tighter interaction and integration of different technologies previously considered as totally separated from an operational perspective. Examples of that trends are the IP and Optical integration (e.g., the introduction of colored interfaces on routers), or the extension of deterministic-behavior features to Layer 3 networks. This kind of convergence in most cases creates dependencies on the conventional network management features, which require to incorporate or integrate functionality from other technological domains.

Furthermore, such convergence is also reflected on the need of interacting and interworking with distinct network parts participating in the end-to-end service delivery. Mobile access, fixed access, data center, enterprise, radio functional split (i.e., fronthaul and midhaul), neutral exchanges, intensive data networks (e.g., scientific academic networks), content distribution, etc., represent network parts constituent of end-to-end services that can impose dependencies of the management of an intermediate network.

That convergence shown the last years also implies the need of an up-to-date refresh of management capabilities and tooling of the conventional networks. Also, it highlights the need to easily map the data models that are used to manage each specific segment.

## Another Item

TBC.

## Another Item

TBC.

# Perspectives & Recommendations

TBC

# Security Considerations

TBC.


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
