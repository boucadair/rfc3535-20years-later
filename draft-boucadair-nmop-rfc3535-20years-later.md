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
   fullname: Luis M. Contreras
   organization: Telefonica
   email: luismiguel.contrerasmurillo@telefonica.com
 -
   fullname: Oscar Gonzalez de Dios
   organization: Telefonica
   email: oscar.gonzalezdedios@telefonica.com
 -
   fullname: Thomas Graf
   organization: Swisscom
   email: thomas.graf@swisscom.com
 -
   fullname: Reshad Rahman
   organization: Equinix
   email: rrahman@equinix.com
 -
   fullname: Lionel Tailhardat
   organization: Orange
   email: lionel.tailhardat@orange.com

normative:

informative:

  ODL:
    title: Graph Model Overview
    date: 2023
    target: https://docs.opendaylight.org/projects/bgpcep/en/latest/graph/graph-user-guide-graph-model.html#
  Widoco2017:
    title: "WIDOCO: a wizard for documenting ontologies"
    date: 2017
    author:
      - name: Daniel Garijo
    target: http://dgarijo.com/papers/widoco-iswc2017.pdf
  LOT2019:
    title: "LOT: An industrial oriented ontology engineering framework"
    date: 2022
    author:
      - name: Maria Poveda-Villalon
      - name: Alba Fernandez-Izquierdo
      - name: Mariano Fernandez-Lopez
      - name: Raul Garcia-Castro
    target: https://doi.org/10.1016/j.engappai.2022.104755

--- abstract

The IAB organized an important workshop
to establish a dialog between network operators and
protocol developers, and to guide the IETF focus on work
regarding network management.  The outcome of that workshop
was documented in the "IAB Network Management Workshop" (RFC 3535)
which was instrumental for developing NETCONF and YANG, in particular.

20 years later, it is time to evaluate what has been achieved since then and
identify the operational barriers for making these
technologies widely implemented. Also, this document captures new
requirements for network management operations.

--- middle

# Introduction

The IAB organized a workshop (June 4-June 6, 2002)
to establish a dialog between network operators and
protocol developers, and to guide the IETF to focus on work
regarding network management.  The outcome of that workshop
was documented in the "IAB Network Management Workshop" {{?RFC3535}}
which was instrumental for developing NETCONF {{?RFC6241}} and YANG {{?RFC6020}}{{?RFC7950}}.

Since the publication of {{?RFC3535}} major advances were achieved in the Network Managment area, such as (but not limited to):

* NETCONF {{?RFC6241}}
* YANG {{?RFC7950}}
* RESTCONF  {{?RFC8040}}
* SDN & Programmable Networks {{?RFC7149}}{{?RFC7426}}
* Automation {{?RFC8969}}
* Virtualization {{?RFC8568}}
* Containerization {{?I-D.ietf-bmwg-containerized-infra}}
* Intent-based {{?RFC9315}}
* Network APIs
* Models for management of services, networks, and devices {{?RFC8199}}{{?RFC8309}}
* Telemetry {{?RFC9232}}
* JSON Encoding of Data Modeled with YANG {{?RFC7951}}
* CoAP Management Interface (CORECONF) {{?I-D.ietf-core-comi}}
* YANG to CBOR mapping {{?RFC9254}}
* YANG Schema Item iDentifier (YANG SID) {{?I-D.ietf-core-sid}}

See also "An Overview of the IETF Network Management Standards" {{?RFC6632}}.

More than 20 years later, new requirements on network management operations are emerging from the operators. This document captures these requirements that reflect the progress in this area. The following table lists the new ops requirements; more details are provided in {{sec-obs}}.

|NEW Ops Requirement Label| Section|
|-------------------------|:------:|
|NEW-OPS-REQ-STRENGTHEN-DM |{{sec-dm}}|
|NEW -OPS-REQ-DM-RATIONALIZE|{{sec-frag}}|
|NEW -OPS-REQ-EASE-EXPOSURE|{{sec-cons}}|
|NEW -OPS-REQ-NW-API-DISCOVERY|{{sec-cons}}|
|NEW-OPS-REQ-DM-API|{{sec-api}}|
|NEW-OPS-REQ-PROFILING|{{sec-pro}}|
|NEW-OPS-REQ-REASSESS|{{sec-pro}}|
|NEW-OPS-REQ-AGILE|{{sec-agile}}|
|NEW-OPS-REQ-INTEGRATION|{{sec-int}}|
|NEW-OPS-REQ-Y2KG|{{sec-dama}}|
|NEW-OPS-REQ-SCALE|{{sec-dama}}|
|NEW-OPS-REQ-LOSSLESS|{{sec-map}}|
|NEW-OPS-REQ-REUSABILITY|{{sec-con}}|
|NEW-OPS-REQ-NEW-NEED|{{sec-distinct}}|
|NEW-OPS-REQ-UNSILO|{{sec-dep}}|
|NEW-OPS-REQ-TIMELY-DM|{{sec-pub}}|
|NEW-OPS-REQ-READILTY-IMPLEM|{{sec-impl}|
|NEW-OPS-REQ-IT-INTEGRATION|{{sec-it}}|
|NEW-OPS-REQ-IETF-TOOLS|{{sec-ietf-in}}|
|NEW-OPS-REQ-CLIENT-TOOLS|{{sec-client}}|
|NEW-OPS-REQ-BRIDGE|{{sec-skills}}|
|NEW-OPS-REQ-GLUE|{{sec-new}}|
|NEW-OPS-REQ-GUIDANCE|{{sec-guid}}|

> Editor note: update the table.

The document also provide an assessment of the RFC3535 recommendations ({{sec-assessment}}) and to what extend that roadmap was driving network management efforts within the IETF ({{sec-reca}}).

# Assessment of RFC 3535 Operator Requirements {#sec-assessment}

## Detailed Analysis

{{Section 3 of ?RFC3535}} includes the following recommendations:

3535-OPS-REQ-EASE-USE:

{:quote}
>      Ease of use is a key requirement for any network management
       technology from the operators point of view.

**Status Update**:
: This is still a valid requirement. It is
       even exacerbated with the amount of techniques and extensions
       that were specified since then.

3535-OPS-REQ-CONFIG-OPS-SEPARATE:

{:quote}
>      It is necessary to make a clear distinction between configuration
       data, data that describes operational state and statistics.  Some
       devices make it very hard to determine which parameters were
       administratively configured and which were obtained via other
       mechanisms such as routing protocols.

**Status Update**:
: This requirement was taken into account when
       designing IETF solutions. Specifically, datastores are a fundamental
       concept in NETCONF/YANG (e.g., {{?RFC8342}}.

3535-OPS-REQ-CONFIG-OPS-FETCH-SEPARATE:

{:quote}
>      It is required to be able to fetch separately configuration data,
       operational state data, and statistics from devices, and to be
       able to compare these between devices.

**Status Update**:
: This is supported by NETCONF and RESTCONF.

3535-OPS-REQ-NETWORK-NOT-DEVICE:

{:quote}
>      It is necessary to enable operators to concentrate on the
       configuration of the network as a whole rather than individual
       devices.

**Status Update**:
: Protocols such as NETCONF supports means to
       handle transactions at the level of a network. For example, a
       controller can establish parallel sessions with a set of devices
       and make use of confirmed commit.
: Also, {{?RFC8969}} describes
       how YANG/RESTONF/YANG can be used to manage a network and map it
       to involves underlying functions/nodes. Several service and network
       data models are required for this aim.
: The IETF defined in the past
       models to manage few servcies such as VPN at both service and network
       levels (e.g.,  the Layer 2 Service Model (L2SM) {{?RFC8466}},
       the Layer 3 Service Model (L3SM) {{?RFC8299}}, the Layer 2 Network Model (L2NM) {{?RFC9291}},
       and the Layer 3 Network Model (L3NM) {{?RFC9182}}).
: A similar effort is currently
       ongoing for handling attachement circuits at both service and network layers (e.g.,
       {{?I-D.ietf-opsawg-teas-attachment-circuit}}, {{?I-D.ietf-opsawg-ntw-attachment-circuit}}).
: More effort is still needed in this area.

3535-OPS-REQ-NETWORK-WIDE-TRANSACTIONS:

{:quote}
>      Support for configuration transactions across a number of devices
       would significantly simplify network configuration management.

**Status Update**:
: This feature is supported by NETCONF.

3535-OPS-REQ-CONFIG-DIFF:

{:quote}
>      Given configuration A and configuration B, it should be possible
       to generate the operations necessary to get from A to B with
       minimal state changes and effects on network and systems.  It is
       important to minimize the impact caused by configuration changes.

**Status Update**:
: This feature is supported by NETCONF.

3535-OPS-REQ-CONFIG-DUMP-RESTORE:

{:quote}
>      A mechanism to dump and restore configurations is a primitive
       operation needed by operators.  Standards for pulling and pushing
       configurations from/to devices are desirable.

**Status Update**:
: This feature is supported by NETCONF.

3535-OPS-REQ-CONFIG-CONSISTENCY-CHECK:

{:quote}
>      It must be easy to do consistency checks of configurations over
       time and between the ends of a link in order to determine the
       changes between two configurations and whether those
       configurations are consistent.

**Status Update**:
: A mechanism is specified in {{?RFC9144}}.

3535-OPS-REQ-CONFIG-NETWORK-WIDE-SCHEMA:

{:quote}
>      Network wide configurations are typically stored in central
       master databases and transformed into formats that can be pushed
       to devices, either by generating sequences of CLI commands or
       complete configuration files that are pushed to devices.  There
       is no common database schema for network configuration, although
       the models used by various operators are probably very similar.
       It is desirable to extract, document, and standardize the common
       parts of these network wide configuration database schemas.

**Status Update**:
: Covered by current implementations.

3535-OPS-REQ-TXT-PROCESSING-TOOLS:

{:quote}
>      It is highly desirable that text processing tools such as diff,
       and version management tools such as RCS or CVS, can be used to
       process configurations, which implies that devices should not
       arbitrarily reorder data such as access control lists.

**Status Update**:
: This is deployment-specific.

3535-OPS-REQ-ACCESS-CONTROL-OPS-CENTRIC:

{:quote}
>      The granularity of access control needed on management interfaces
       needs to match operational needs.  Typical requirements are a
       role-based access control model and the principle of least
       privilege, where a user can be given only the minimum access
       necessary to perform a required task.

**Status Update**:
: RBAC is supported by existing implementation. Also,
       the IETF defined {{?RFC8341}} for this purpose.

3535-OPS-REQ-ACCESS-CONTROL-CHECKS:

{:quote}
>      It must be possible to do consistency checks of access control
       lists across devices.

**Status Update**:
: This is implementation-specific.

3535-OPS-REQ-CONFIG-SEPARATE-DISTRIB-ACTIV:

{:quote}
>      It is important to distinguish between the distribution of
       configurations and the activation of a certain configuration.
       Devices should be able to hold multiple configurations.

**Status Update**:
: This is supported by existing NETCONF methods.

3535-OPS-REQ-ACCESS-CONTROL-BOTH-DATA-TASK:

{:quote}
>      SNMP access control is data-oriented, while CLI access control is
       usually command (task) oriented.  Depending on the management
       function, sometimes data-oriented or task-oriented access control
       makes more sense.  As such, it is a requirement to support both
       data-oriented and task-oriented access control.

**Status Update**:
: This is supported by {{?RFC8341}}.

## Summary

|RFC3535 Ops Requirement Label       | Status                                    |
|-----------------------------------:|:------------------------------------------|
| 3535-OPS-REQ-EASE-USE                      | Still Applicable                          |
| 3535-OPS-REQ-CONFIG-OPS-SEPARATE           | OK                                        |
| 3535-OPS-REQ-CONFIG-OPS-FETCH-SEPARATE     | OK                                        |
| 3535-OPS-REQ-NETWORK-NOT-DEVICE            | Protocol (OK), DM (Still Applicable)      |
| 3535-OPS-REQ-NETWORK-WIDE-TRANSACTIONS     | OK                                        |
| 3535-OPS-REQ-CONFIG-DIFF                   | OK                                        |
| 3535-OPS-REQ-CONFIG-DUMP-RESTORE           | OK                                        |
| 3535-OPS-REQ-CONFIG-CONSISTENCY-CHECK      | Implementation-specific                   |
| 3535-OPS-REQ-CONFIG-NETWORK-WIDE-SCHEMA    | Still Applicable                          |
| 3535-OPS-REQ-TXT-PROCESSING-TOOLS          | Deployment-specific                       |
| 3535-OPS-REQ-ACCESS-CONTROL-OPS-CENTRIC    | Implementation-specific                   |
| 3535-OPS-REQ-ACCESS-CONTROL-CHECKS         | Implementation-specific                   |
| 3535-OPS-REQ-CONFIG-SEPARATE-DISTRIB-ACTIV | OK                                        |
| 3535-OPS-REQ-ACCESS-CONTROL-BOTH-DATA-TASK | OK                                        |

# Assessment of RFC 3535 Recommendations {#sec-reca}

## Detailed Analysis

{{Section 6 of ?RFC3535}} includes the following recommendations:

3535-RECO-STOP-MANDATE-MIB:

{:quote}
>      The workshop recommended that the IETF stop forcing working groups
       to provide writable MIB modules.  It should be the decision of
       the working group whether they want to provide writable objects
       or not.

**Status Update**:
: In 2014, the IESG published a statement Writable MIB Module, which states that:

   > SNMP MIB modules creating and modifying configuration state should only be produced by working groups in cases of clear utility and consensus to use SNMP
 write operations for configuration, and in consultation with the OPS ADs/MIB doctors.

3535-RECO-MIB-INVESTIGATE:

{:quote}
>      The workshop recommended that a group be formed to investigate why
       current MIB modules do not contain all the objects needed by
       operators to monitor their networks.

**Status Update**:
: No such group was formed to our knowledge.

3535-RECO-SNMP-WG4MONITORING:

{:quote}
>      The workshop recommended that a group be formed to investigate why
       the current SNMP protocol does not satisfy all the monitoring
       requirements of operators.

**Status Update**:
: No such group was formed to our knowledge.
: This SNMP shortcoming was also reiterated in {{Section 3.5.2 of ?RFC5345}}.

3535-RECO-FOCUS-IETF-CONFIG-MECHANISMS:

{:quote}
>      The workshop recommended, with strong consensus from both protocol
       developers and operators, that the IETF focus resources on the
       standardization of configuration management mechanisms.

**Status Update**:
: NETCONF {{?RFC6241}}, RESTCONF {{?RFC8040}}, CORECONF {{I-D.ietf-core-comi}}, YANG.
: YANG is a transport-independent data modeling language. It can be used independently of NETCONF/RESTCONF. For example, YANG can be used to define abstract data structures {{?RFC8791}} that can be manipulated by other protocols (e.g., {{?RFC9132}}).

3535-RECO-FOCUS-XML:

{:quote}
>      The workshop recommended, with strong consensus from the operators
       and rough consensus from the protocol developers, that the
       IETF/IRTF should spend resources on the development and
       standardization of XML-based device configuration and management
       technologies (such as common XML configuration schemas, exchange
       protocols and so on).

**Status Update**:
: OK. This recommendation was also mirrored in other documents such as {{?RFC5706}}.

3535-RECO-NO-HTTP:

{:quote}
>      The workshop recommended, with strong consensus from the operators
       and rough consensus from the protocol developers, that the
       IETF/IRTF should not spend resources on developing HTML-based or
       HTTP-based methods for configuration management.

 **Status Update**:
 : The IETF deviated from this recommendation, e.g., RESTCONF {{?RFC8040}} or CoAP Management Interface (CORECONF) {{?I-D.ietf-core-comi}}.

3535-RECO-MAINTAIN-SMI-SPPI:

 {:quote}
>      The workshop recommended, with rough consensus from the operators
       and strong consensus from the protocol developers, that the IETF
       should continue to spend resources on the evolution of the
       SMI/SPPI data definition languages as being done in the SMIng
       working group.

**Status Update**:
: SMIng WG was concluded in 2003-04-04.

3535-RECO-IETF2FIX-MIB:

{:quote}
>      The workshop recommended, with split consensus from the operators
       and rough consensus from the protocol developers, that the IETF
       should spend resources on fixing the MIB development and
       standardization processs.

**Status Update**:
: The IETF dedicated some resources to fix some SNMP shortcomings with a focus on security (e.g., Transport Layer Security (TLS) Transport Model for the SNMP {{?RFC6353}} or {{?RFC9456}}, HMAC-SHA-2 Authentication Protocols in User-Based Security Model (USM) for SNMPv3 {{?RFC7860}}).

{{Section 6 of ?RFC3535}} also includes the following but without tagging them as recommendations:

3535-MISC-NO-CIM:

{:quote}
>      The workshop had split consensus from the operators and rough
       consensus from the protocol developers, that the IETF should not
       focus resources on CIM extensions.

**Status Update**:
: The IETF didn't dedicate any resources on CIM extensions.

3535-MISC-ABANDON-PIB:

{:quote}
>      The workshop had rough consensus from the protocol developers
       that the IETF should not spend resources on COPS-PR development.
       So far, the operators have only very limited experience with
       COPS-PR.  In general, however, they felt that further development
       of COPS-PR might be a waste of resources as they assume that
       COPS-PR does not really address their requirements.

**Status Update**:
: The IETF has reclassified COPS Usage for Policy Provisioning {{?RFC3084}}
  to Historic status.

3535-MISC-ABANDON-COPS-PR:

{:quote}
>      The workshop had rough consensus from the protocol developers
       that the IETF should not spend resources on SPPI PIB definitions.
       The operators had rough consensus that they do not care about
       SPPI PIBs.

**Status Update**:
: The IETF has reclassified Structure of Policy Provisioning Information {{?RFC3159}}, as well as
  three Policy Information Bases ({{?RFC3317}}, {{?RFC3318}}, and {{?RFC3571}}) to
  Historic status.

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


# Observations and New Requirements {#sec-obs}

## On the Importance of Data Models {#sec-dm}

An appealing aspect about network automation techniques is that they almost apply to any kind of network. From that perspective, the functional component of a network automation framework that probably matters the most, and independent of the underlying interfaces and protocols, are the data models. Concretely, data models are instrumental in the automation of networks, especially that they can provide closed-loop control for adaptive and deterministic service creation, delivery, and maintenance.

Data models can be used to derive required configuration information for both network and service components, and state information that will be monitored and tracked. Likewise, they can be used during the service/network management life cycle (e.g., service instantiation, provisioning, optimization, monitoring, diagnostic, and assurance).

More than three decades of "Internet standardization" have shown that the specification of data models is not that straightforward. This is because of at least two major reasons:

*	For more than 30 years, legacy network equipment manufacturers have considered their technology as a competitive advantage, thereby leading to proprietary, vendor-specific, data models and the burden of vendor lock-ins. For example, there are more YANG proprietary modules than standarized ones.

*	Over the same period, operators have also developed their savoir-faire as a key competitive advantage. Such savoir-faire had to rely upon these proprietary data models. Operators were reluctant in the past to share their design and management practices.

The situation has  changed since network "softwarization" strategies have been disclosed by vendors and operators. From a business standpoint, network "softwarization" is seen as a major transformation effort by operators, because of the flexibility and the "a la carte" approach that is promoted by "X-as-a-service" (XaaS) designs, "X" being network, platform, Network Slice, etc.

XaaS designs assume the availability of data models that are dynamically instantiated (along with a set of relevant policies) as a function of the "X" (and its design, for that matter). **XaaS services cannot be designed, delivered, and operated without data models.** Standard data models are thus key as they allow to:

*	Ease mapping among many (network/service) layers.
*	Ease data correlation from distinct sources.
*	Nullify (soften) CLI specifics to vendors.
*	Support both top-down and bottom-up approaches:

  - Accurate control loops for adaptive and deterministic service creation, delivery, and maintenance.
  - Feed an intelligence that will drive appropriate actions to adjust the current status to align with the intended status.

NEW-OPS-REQ-STRENGTHEN-DM:
: Network softwarization can only happen with a strong, committed standardization effort, complemented by active involvement in open-source projects that facilitate access to code.
: Particularly, **without data models, a Network API is essentially useless** (see also {{sec-api}}).

## Fragmented Ecosystem {#sec-frag}

The current YANG device models ecosystem is **fragmented**: some standards models are defined through the IETF, while similar ones are defined in other forums such as Openconfig or ONF.
Unlike service and network models, IETF-defined device models are not widely implemented.

NEW-OPS-REQ-DM-RATIONALIZE:
: There is a need to rationalize this space and avoid redundant efforts.

## The Network Becomes Consumable {#sec-cons}

Network connectivity can support tailored services in terms of Service Level Obejctives (SLOs), for instance, by means of Network Slice Services {{?RFC9543}}. This approach of "consuming" the network flexibly and dynamically is made possible by enabling means of exposing network capabilities to either internal or external applications. Then, network management is no longer limited to collect network status information, but it should be now extended to permit the exposure of resources, capabilities, functionality, and associated information (e.g., inventory based data).

NEW-OPS-REQ-EASE-EXPOSURE:
: Focus on protocols and data models to expose network/service capabilities, network-wide services, and related operations.

NEW-OPS-REQ-NW-API-DISCOVERY:
: Define a reference approach/process for service exposure discovery (APIs discovery).

## Network APIfication {#sec-api}

APIs are getting momentum as means of interworking between parties, also at the time of providing network services. As an example, {{?I-D.ramseyer-grow-peering-api}} defines an API for dynamically establishing BGP peering sessions between Autonomous Systems of different administrative domains. That same objective is also covered by the YANG data model defined in {{?I-D.ietf-opsawg-teas-attachment-circuit}} as exemplified in Appendix A.10. Tools such as YANG/OpenAPI transforms are key to leverage existing data models and allow for better integration and mapping to actual realization models.

NEW-OPS-REQ-DM-API:
: Readily available API specifications could be generalized from YANG modules for fast development, prototyping, and validation.

## Lack of Profiling {#sec-pro}

Many NETCONF-related features are (being) specified by the IETF, but these features are not widely supported (e.g., YANG-Push {{?RFC8639}}).

NEW-OPS-REQ-PROFILING:
: Editing a profile document that outlines a set of recommendations for core/key features, along with appropriate justifications, will help foster more implementations that meet operators’ needs.

> Examples of such profile documents are the various RFCs that were published by the Behavior Engineering for Hindrance Avoidance (behave) WG {{?BCP127}}.
> Another approach could be to consider a model similar to the "Roadmap for Transmission Control Protocol (TCP) Specification Documents" {{?RFC7414}}.
> Such a document would serve as a guide and reference for implementers and others seeking information on 'NETCONF/RESTCONF/YANG'-related RFCs.

NEW-OPS-REQ-REASSESS:
: Additionally, reassessing the value of some IETF proposals compared to competing or emerging solutions (e.g., gRPC vs. YANG-Push) would be beneficial.

## Lack of Agile Process for (The Maintenance of) YANG Modules {#sec-agile}

RFCs might not be suited for documenting YANG modules (it takes much too long, especiallly for updates). In the meantime, there is a need for "reference models" and "sufficiently stable models".

An hybrid approach might be investigated for documenting IETF-endorsed YANG modules, such as considering an RFC to describe the initial module sketch and objectives and an official IETF repository for maintaining intermediate YANG versions.

By drawing a parallel between YANG data models and the concept of ontology used in the field of Semantic Web, the topic of YANG module maintenance could greatly benefit from proven methodologies in knowledge engineering such as {{LOT2019}} and automatic documentation tools like {{Widoco2017}}.

NEW-OPS-REQ-AGILE:
: Develop a more agile process for the development and maintenance of YANG modules in the IETF.

## Integration Complexity {#sec-int}

{{Section 3 of ?RFC3535}} describes a set of network operator requirements. One of the requirements is the ease of use which, according to {{Section 3.2 of ?RFC6244}}, is addressed by NETCONF and YANG. For configuration this holds true, for network observability it is unfortunately not yet. This has been confirmed with a set of network operators asking how long it takes from subscribing YANG data to make it accessible to the operator. Minutes, Hours, Days, or Weeks. None of them answered Minutes or Hours. All of them responded Days or Weeks. Hinting manual post processing of YANG data.

Collecting YANG metrics from networks is already a struggle due to late arrival of {{?RFC8639}}, {{?RFC8640}}, {{?RFC8641}}, {{?I-D.ietf-netconf-https-notif}}, and {{?I-D.ietf-netconf-udp-notif}} for configured subscription transport protocols which defined YANG-Push in the industry. This caused network vendors to implement alternative solutions to collect real-time streaming data in the meanwhile, such as gNMI which was proposed in 2018 in {{?I-D.openconfig-rtgwg-gnmi-spec}} to the IETF but not followed up on. Unfortunately, these implementations differ between network Operating Systems due to the lack of standardization, specifically for the metadata which would ensure machine readability.

When a set of network operators where asked to where operational YANG data needs to be integrated to, the answer homogeneously was Apache Kafka Message Broker and Time Series Databases. There is a need to specify how YANG-Push can be integrated into Apache Kafka and references needed YANG-Push extensions and YANG schema registry development. The YANG-Push extensions addressing needs to make YANG-Push messages machine readable and against semantic validate able to ensure a consistent data processing.

Another challenge is that the subscribed YANG data referenced with datastore-subtree-filter or datastore-xpath-filter breaks semantic integrity which needs to be addressed by either updating {{Section 4 of ?RFC8641}} or proposing a new YANG module being used at the YANG-Push receiver.

NEW-OPS-REQ-INTEGRATION:
: Consider approaches to ease integration by-design (e.g., protocols and data models).

## YANG-formatted Data Manipulation {#sec-dama}

The use of a flat tree hierarchy in YANG models may induce some performance issues compared to other graph models.
This can be the case, for example, during a path calculation on a network topology.
Different approaches using graph theory and compatible with YANG are currently available, but require further experimentation to generalize their adoption.
For instance, {{ODL}} implements an in-memory connected graph version of YANG-based data to enable fast breadth-first search (BFS).

NEW-OPS-REQ-Y2KG:
: Need for a reference specification to translate YANG-based data into the knowledge graph (KG).

For example, {{?I-D.marcas-nmop-knowledge-graph-yang}} and {{?I-D.tailhardat-nmop-incident-management-noria}} discuss YANG-2-KG proposals to leverage automated reasoning and graph traversal techniques.

NEW-OPS-REQ-SCALE:
: Consider approaches for YANG models to scale.

## Translation and Mapping Between Service/Network and Device Models {#sec-map}

Navigating among multiple levels of the hierarchy (service, network, device) relies
currently on proprietary solutions to graft and translate between two layers. There
is no programmatic approach to ensure lossless mappings.

NEW-OPS-REQ-LOSSLESS:
: Consider programmatic approaches to ensure lossless mappings between service/network/device data models.

## (In)Consistent Data Structures in Network Protocols for Data Export {#sec-con}

Network Telemetry, as described in {{?RFC9232}}, involve a set of protocols. Due to the different requirements, one Network Telemetry protocol doesn't address all needs. This is mainly due to the nature of the subscribed data. BGP Monitoring Protocol (BMP) {{?RFC7854}} adds monitoring and tracing capabilities natively to the BGP process to minimize the processing overhead. While IPFIX {{?RFC7011}}{{?RFC7012}} can be applied according to {{?RFC5472}} to gain visibility into the data and forwarding planes, due to the amount of data, sampling as defined in {{?RFC5476}} and applied to IPFIX in {{?RFC5477}} and aggregation as defined in {{?RFC7015}} for IPFIX is needed to reduce the amount of exposed data. While YANG-Push focuses on exposing already YANG modelled data, which eases the correlation among network configuration and operational data.

{{?RFC9232}} is an informational document and does not specify what these Network Telemetry protocols should have in common to ensure consistent data structures for data export. While data types are fairly good aligned, a lack of metadata standardization among the Network Telemetry protocols is observed. In particular describing from where the metrics has been exported from and timestamping. In {{Section 4.2 of ?RFC7854}} timestamps are optional and sysName {{?RFC1213}} is only carried in the BMP initiation message ({{Section 4.3 of ?RFC7854}}), while the message header of IPFIX defined in {{Section 4.3 of ?RFC7011}} lacks the sysName definition.

The lack of information from where the data is being pushed from is only known to the Network Telemetry data collection due to the transport session being established from the network node exporting the information. When Network Telemetry messages are being transformed and forwarded, this information is being lost. Therefore, it is common among network operators to augment sysName and other metadata at the data collection.

The same common principle applies to when observation timestamping is missing in the Network Telemetry message. Since the data collection is the closest element to the network, a time stamp is added to give the network operator at least the information when the Network Telemetry message was collected. However, since Network Telemetry addresses real-time streaming needs, this is often not accurate enough for data correlation.

NEW-OPS-REQ-REUSABILITY:
: Consider approach to ensure reuse/consistent data structure.

## Proprietary YANG Modules, CLI, and Limited Abstraction {#sec-limit}

Leveraging on pluggins, propietary YANG models or even CLI is still the rule in many operations, sometimes forced by the need of operating legacy infrastructures.

The complexity of developing and maintaining these means of operation is huge, as it is required to to cover many OS and vendors along the lifetime of the network device.

Network models for the realization of services provide some "level" of abstraction and then automation.

## Distinct Networks, Distinct Management Requirements {#sec-distinct}

From the time {{?RFC3535}} was released up to now, new kind of services and applications have been developed and deployed over the time, with very diverse, and some times contradicting, requirements. Those services have been engineered on top of multi-service networks for the sake of efficiency and simplicity, accommodating such a variety of needs. As a result, services requiring mobility, data replication, large capacity, adaptability, multi-path support, determinism, etc., coexist on the same shared network, needing from it mechanisms for graceful operation.

Likewise, such diversity of services also require different management capabilities. For example, session continuity, distribution trees, traffic engineering, congestion status notification, reordering, or on-time delivery impose very different management needs to be satisfied.

This reality is different from the one existing at the time of {{?RFC3535}}, and as such, the new identified needs can require from novel approaches to guarantee the aforementioned co-existence of services.

NEW-OPS-REQ-NEW-NEED:
: Some networks have specific network management requirements such as the need for asynchronous operations or constraints on data compactness. An example of such networks is Delay-Tolerant Networking (DTN) {{?RFC838}} or DetNet {{?RFC8557}}.

## Implications of External Dependency {#sec-dep}

Networks are being updated to abandon the silo approach from the past towards an increasing convergence. Specifically, there are trends towards a tighter interaction and integration of different technologies previously considered as totally separated from an operational perspective. Examples of that trends are the IP and Optical integration (e.g., the introduction of colored interfaces on routers), or the extension of deterministic-behavior features to Layer 3 networks. This kind of convergence in most cases creates dependencies on the conventional network management features, which require to incorporate or integrate functionality from other technological domains.

Such convergence is also reflected on the need of interacting and interworking with distinct network parts participating in the end-to-end service delivery. Mobile access, fixed access, data center, enterprise, radio functional split (i.e., fronthaul and midhaul), neutral exchanges, intensive data networks (e.g., scientific academic networks), content distribution, etc., represent network parts constituent of end-to-end services that can impose dependencies of the management of an intermediate network.

NEW-OPS-REQ-UNSILO:
: The convergence observed in recent years also implies the need for an up-to-date refresh of management capabilities and tools for conventional networks.
: It highlights the necessity to handle the heterogeneity of data, configuration, and network management/requirements.
: From a YANG perspective, this involves easily mapping and relating the data models used to manage each specific segment.
: Resolving such issue could draw on insights from parallel technical fields such as knowledge engineering practices and concepts associated with Linked Data in the Semantic Web, areas where it is common to manage problems of heterogeneity and data reconciliation across various application domains.

## Too Much Time Between Publication of New Networking Functionality and the Associated YANG {#sec-pub}

For example, {{?RFC8667}} (IS-IS extensions for SR) was published in December 2019, while {{?I-D.ietf-isis-sr-yang}} will be published ~5 years after.

NEW-OPS-REQ-TIMELY-DM:
: Consider having YANG as part of the protocol specification/change where possible, or have the YANG document progress in parallel.
That may slow down the protocol specification, though.

## Lack of Implementation of Proposed Solutions {#sec-impl}

New solutions proposed by WGs such as NETMOD and NETCONF very often lack an implementation or only have a partial implementation. The situation has improved with the last hackathons (e.g., for YANG-Push), but these solutions became RFCs without a known implementation:

* YANG-Push {{?RFC8641}}
* Schema-mount {{?RFC8528}}
* NMDA {{?RFC8342}}

Schema-mount allegedly has only one known implementation because of the complexity of the solution. That means the IETF most likely spent lots of cycles for something which won't be deployed ever.

While hackathons have improved the situation, the availablability of implementation is concerning. For open-source, 'sysrepo'/'libyang' are decent choices.

NEW-OPS-REQ-READILTY-IMPLEM:
: It is tempting to consider mandating at least one implementation. However, there were areas which imposed in the past rules for implementations for I-Ds to be published as PS (e.g., {{?RFC1264}}), but these rules were relaxed for reasons described, e.g., {{?RFC4794}} and left it to the WGs to decide about the actual measures to put in place. To date, only IDR WG has clear guidance on two implementations.

## Tooling & Skills

### Integration with "native" IT Tooling {#sec-it}

NEW-OPS-REQ-IT-INTEGRATION:
: There is a need to ease the integration of low-level/network-oriented solution with native "IT tooling" (e.g., "https://opentelemetry.io/").

### IETF Support for Better YANG Integration {#sec-ietf-in}

NEW-OPS-REQ-IETF-TOOLS
: Ease exposure of libraries and host tools (e.g., `yangkit`) to ease integration.

### Open-source Tools {#sec-client}

While there are open-source implementations for NETCONF (e.g., NETOPEER), the gRPC/gNMI suite seems to have more support for tools on the client side.
For example, "ygot" generates structures from YANG models and these can easily be used by a client to configure a device with gNMI. NETCONF is not supported though (we need the XML tags).

NEW-OPS-REQ-CLIENT-TOOLS:
: Focus on tooling is needed, especially on the client side.

### Skills {#sec-skills}

The IETF is not the expert community in data engineering. The experts are in the data industry. Without them, integration in data processing chains like Data Mesh is going to be a challenge.

NEW-OPS-REQ-BRIDGE:
: Create an eco-system where data and networking engineers can collaborate.

## New Service Approaches {#sec-new}

The virtualization trend have made posible to dynamically instantiate Service Functions (SFs) in distributed compute facilities in the form of virtual machines or containers, as micro-services. The instantiation of the SFs is governed by cloud management systems, as it is the connectivity among the different instances or micro-services. That connectivity is typically realized by using overlay mechanisms, without any further interaction with the network. However, this appraoch seems to be insuficient for future services demanding stringent requirements in terms of SLOs.

NEW-OPS-REQ-GLUE:
: The distinct approaches followed in both the compute and the network environments makes necessary to define suitable mechanisms for enabling an efficient interplay, while highly automating the overall service delivery procedure.

## Many Solutions for the Same Problem, but Lack of Clear Applicably Guidance {#sec-guid}

There are several solutions that were standardized for network management purposes. For example, management of ACLs by means to BGP FlowSpec {{?RFC8955}}{{?RFC8956}} or  by means of NETCONF/YANG {{?RFC8519}}. There is no cross referencing between the two standards or delimits its applicability scope vs the other approach.

NEW-OPS-REQ-GUIDANCE:
: The target application/applicability of a network management approach should be integrated in the specification itself.

# New Requirements

## Summary

NEW-OPS-REQ-STRENGTHEN-DM:
: Network softwarization can only happen with a strong, committed standardization effort, complemented by active involvement in open-source
projects that facilitate access to code.

NEW-OPS-REQ-DM-RATIONALIZE:
: Rationalize this space and avoid redundant efforts (in almost all layers (IP, optic, etc.)). Unlike service and network models, Standard-based device models are not widely implemented.

NEW-OPS-REQ-QUICK-BUT-WELL:
: Develop a more agile process for the development and maintenance of YANG modules in the IETF. RFCs might not be suited for documenting YANG modules.

NEW-OPS-REQ-GUIDE-AND-PROFILE:
: The target application/applicability of a network management approach should be documented (e.g., edit profile documents that outline a set of recommendations for core/key features, along with appropriate justifications, will help foster more implementations that meet operators’ needs). This also covers security management aspects of network management. Additionaly, consider independent compliance suites to validate functions/features/etc.

NEW-OPS-REQ-ARCH:
: Need to promote more arch and framework documents to exemplify the intended use.

NEW-OPS-REQ-EASE-EXPOSURE:
: Focus on protocols and data models to expose network/service capabilities, network-wide services, and related operations.

NEW-OPS-REQ-TIMELY-DM:
: Consider having YANG as part of the protocol specification/change where possible, or have the YANG document progress in parallel.

NEW-OPS-REQ-READILY-IMPLEM:
: The availablability of implementation is concerning. Consider catalyst approaches to trigger more (open) implementations, especially during the development of protocols/extensions.

NEW-OPS-REQ-DM2API:
: Readily available API specifications should be generalized from YANG modules for fast development, prototyping, and validation.

NEW-OPS-REQ-NW-API-DISCOVERY:
: Define a reference approach/process for service exposure discovery (APIs discovery).

NEW-OPS-REQ-REASSESS:
: Reassess the value of some IETF proposals, including compared to competing or emerging solutions (e.g., gNMI).

NEW-OPS-REQ-BRIDGE:
: Create an eco-system where data and networking engineers can collaborate.

NEW-OPS-REQ-INTEGRATION:
: Consider approaches to ease integration by-design (e.g., protocols and data models). The integration covers both horizontal and vertical realms. For example, there is a lack of enablement of this integration across standard bodies that operators are left to solve.

NEW-OPS-REQ-LOSSLESS:
: Consider programmatic approaches to ensure lossless mappings between service/network/device data models. Means to detect, characterize, and expose loss may be considered. Note that lossless mapping is a enabler for support of deterministic verification, auditing, and tracing back along layers/models.

NEW-OPS-REQ-REUSABILITY:
: Consider approaches to ensure reuse/consistent data structure across various NM segments. This will ease correlating data learned from different means (IPFIX, BMP, SYSLOG, etc.).

NEW-OPS-REQ-SCALE:
: Consider approaches for YANG models to scale + protocol considerartions (transactions, touches, etc.). Specifically, address Telemetry scalability enhancements.

NEW-OPS-REQ-UNSILO:
: Necessity to handle the heterogeneity of data, configuration, and network management/requirements. Resolving such issue could draw on insights from parallel technical fields such as knowledge engineering practices and concepts associated with Linked Data in the Semantic Web, areas where it is common to manage problems of heterogeneity and data reconciliation across various application domains.

NEW-OPS-REQ-IT-INTEGRATION:
: There is a need to ease the integration of low-level/network-oriented solution with native "IT tooling" (e.g., "https://opentelemetry.io/").

NEW-OPS-REQ-ITER:
: Need a velocity and approach to standardisation that allows for business goals to be incrementally realised.

NEW-OPS-REQ-Y2KG:
: Need for reference specifications to translate YANG-based data into the knowledge graph. Sample use cases to illustrate the intended use should be considered as well.

NEW-OPS-REQ-TOOLS:
: Focus on tooling is needed, especially on the client side. There is a need for tools that are easy to use. Likewise, there is need for support for multiple friendly, stable, and feature-rich libraries for programming languages.

NEW-OPS-REQ-IETF-TOOLS:
: Ease exposure of libraries and host tools (e.g., yangkit) to ease integration.

NEW-OPS-REQ-NEW-NEED:
: Some networks have specific network management requirements such as the need for asynchronous operations or constraints on data compactness.

NEW-OPS-REQ-GLUE:
: Distinct approaches followed in both the compute and the network environments make necessary to define suitable mechanisms for enabling an efficient interplay, while highly automating the overall service delivery procedure.

## Categorization

|NEW Ops Requirement Label   | DM       | Protocol     | Deployability  | Integration    |SDO Process| Collaboration & Cooperation  | Skills         |
|----------------------------|:--------:|:------------:|:--------------:|:--------------:|:---------:|:----------------------------:|:--------------:|
|NEW-OPS-REQ-STRENGTHEN-DM   |	X	    |	             |      X		   |	              |           |	                           |                |
|NEW-OPS-REQ-DM-RATIONALIZE  |	X		 |              |      X 		   |                |    X      |            X                 |                |
|NEW-OPS-REQ-QUICK-BUT-WELL  |	X   	 |     X        |      X		   |                |           |            	               |                |	
|NEW-OPS-REQ-GUIDE-PROFILE   |	X  	 |     X        |      X		   |                |           |            	               |                |			
|NEW-OPS-REQ-ARCH            |			 |     X        |      X		   |                |           |            	               |                |		
|NEW-OPS-REQ-EASE-EXPOSURE   |	X   	 |     X        |      X		   |      X         |           |            	               |                |	
|NEW-OPS-REQ-TIMELY-DM       |	X		 |              |      X		   |                |           |            	               |                |		
|NEW-OPS-REQ-READILY-IMPLEM  |	X		 |     X        |      X		   |                |    X      |            	               |                |	
|NEW-OPS-REQ-DM-API          |			 |              |      X		   |                |           |            	               |                |
|NEW-OPS-REQ-NW-API-DISCOVERY|			 |              |      X		   |      X         |           |            	               |                |	
|NEW-OPS-REQ-REASSESS        |			 |     X        |       		   |                |           |            	               |                |	
|NEW-OPS-REQ-BRIDGE          |			 |              |       		   |                |           |            X                 |      X         |
|NEW-OPS-REQ-INTEGRATION     |			 |              |      X		   |      X         |    X      |            	               |                |
|NEW-OPS-REQ-LOSSLESS        |			 |              |      X		   |      X         |    X      |            	               |                |	
|NEW-OPS-REQ-REUSABILITY     |			 |      X       |       		   |      X         |    X      |            	               |                |
|NEW-OPS-REQ-SCALE           |	X   	 |      X       |       		   |                |           |            	               |                |
|NEW-OPS-REQ-UNSILO          |			 |              |      X		   |      X         |           |            	               |                |	
|NEW-OPS-REQ-IT-INTEGRATION  |			 |              |      X		   |      X         |           |            	               |                |
|NEW-OPS-REQ-ITER            |			 |              |       		   |                |    X      |            X                 |                |
|NEW-OPS-REQ-Y2KG            |			 |              |      X		   |      X         |           |            	               |                |
|NEW-OPS-REQ-TOOLS           |			 |              |      X		   |      X         |           |            	               |        X       |
|NEW-OPS-REQ-IETF-TOOLS      |			 |              |       		   |                |    X      |            	               |        X       |
|NEW-OPS-REQ-NEW-NEED        |			 |      X       |       		   |                |           |            	               |                |
|NEW-OPS-REQ-GLUE            |			 |              |       		   |      X         |           |            	               |        X       |

## Overall New Requirements Levels (Operators)

|NEW Ops Requirement Label    | Overall Level  |
|----------------------------:|:--------------:|
|NEW-OPS-REQ-STRENGTHEN-DM    |    Strong      |
|NEW-OPS-REQ-DM-RATIONALIZE   |    Strong      |
|NEW-OPS-REQ-QUICK-BUT-WELL   |    Strong      |
|NEW-OPS-REQ-GUIDE-AND-PROFILE|  Nice to have  |
|NEW-OPS-REQ-ARCH             |    Strong      |
|NEW-OPS-REQ-EASE-EXPOSURE    |    Strong      |
|NEW-OPS-REQ-TIMELY-DM        |    Strong      |
|NEW-OPS-REQ-READILY-IMPLEM   |    Strong      |
|NEW-OPS-REQ-DM2API           |    Strong      |
|NEW-OPS-REQ-NW-API-DISCOVERY |  Nice to have  |
|NEW-OPS-REQ-REASSESS         |    Strong      |
|NEW-OPS-REQ-BRIDGE           |    Strong      |
|NEW-OPS-REQ-INTEGRATION      |    Strong      |
|NEW-OPS-REQ-LOSSLESS         |  Nice to have  |
|NEW-OPS-REQ-REUSABILITY      |    Strong      |
|NEW-OPS-REQ-SCALE            |    Strong      |
|NEW-OPS-REQ-UNSILO           |    Strong      |
|NEW-OPS-REQ-IT-INTEGRATION   |  Nice to have  |
|NEW-OPS-REQ-ITER             |    Strong      |
|NEW-OPS-REQ-Y2KG             |  Nice to have  |
|NEW-OPS-REQ-TOOLS            |    Strong      |
|NEW-OPS-REQ-IETF-TOOLS       |  Nice to have  |
|NEW-OPS-REQ-NEW-NEED         |  Nice to have  |
|NEW-OPS-REQ-GLUE             |  Nice to have  |

## Collaborative Prioritization

> TBC to reflect the priorities set by the WG.

> ((Including Rob's Inputs))

* Move much faster (NEW-OPS-REQ-QUICK-BUT-WELL, NEW-OPS-REQ-TIMELY-DM)
* Implement minimal functionality, not bells and whistles (NEW-OPS-REQ-GUIDE-AND-PROFILE, NEW-OPS-REQ-ITER)
* Have running code (NEW-OPS-REQ-READILY-IMPLEM, NEW-OPS-REQ-TOOLS)
* Have vendors and operators on board at the time of developing the solution independent compliance suite to validate things.
* Need to coorelating data learned from different means (IPFIX, BMP, Models)

# Security Considerations

This document does not define any protocol or architecture.

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

Thanks to Christian Jacquenet and Jean-Michel Combes for their inputs.
