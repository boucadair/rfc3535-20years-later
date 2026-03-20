---
title: "An Update of Operators Requirements on Network Management Protocols and Modelling"
abbrev: "RFC 3535, 20 Years Later"
category: info

docname: draft-ietf-nmop-rfc3535-20years-later-latest
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

contributor:
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
  OC:
    title: Openconfig
    date: false
    target: https://www.openconfig.net/
  CAMARA:
    title: CAMARA
    date: false
    target: https://camaraproject.org/
  YC:
    title: YANG Catalog, YANG Modules Stats
    date: 2026
    target: https://www.yangcatalog.org/private-page
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

This document identifies a list of operators requirements for network management operations.
These requirements reflect advances in this field since the publication of "IAB Network Management Workshop" (RFC 3535), which
was instrumental for developing many key technologies that are widely deployed.

--- middle

# Introduction

The IAB organized a workshop (June 4-June 6, 2002)
to establish a dialog between network operators and
protocol developers, and to guide the IETF to focus on work
regarding network management.  The outcome of that workshop
was documented in the "IAB Network Management Workshop" {{!RFC3535}}
which was instrumental for developing NETCONF {{?RFC6241}} and YANG {{?RFC6020}}{{?RFC7950}}, in particular.

Since the publication of {{!RFC3535}} major advances were achieved in the network managment area, such as (but not limited to):

* NETCONF {{?RFC6241}}
* YANG {{?RFC7950}}
* RESTCONF  {{?RFC8040}}
* SDN and Programmable Networks {{?RFC7149}}{{?RFC7426}}
* Automation {{?RFC8969}}
* Virtualization {{?RFC8568}}
* Containerization {{?I-D.ietf-bmwg-containerized-infra}}
* Intent-based {{?RFC9315}}
* Network APIs (e.g., {{CAMARA}})
* Models for management of services, networks, and devices {{?RFC8199}}{{?RFC8309}}
* Telemetry {{?RFC9232}}
* JSON Encoding of Data Modeled with YANG {{?RFC7951}}
* CoAP Management Interface (CORECONF) {{?I-D.ietf-core-comi}}
* YANG to CBOR mapping {{?RFC9254}}
* YANG Schema Item iDentifier (YANG SID) {{?I-D.ietf-core-sid}}

See also "An Overview of the IETF Network Management Standards" {{?RFC6632}}.

More than 20 years later after the publication of {{!RFC3535}}, new requirements on network management operations are emerging from the operators. This document captures these requirements that reflect the progress in this area. Readers may also refer to {{?I-D.iab-nemops-workshop-report}}.

# Observations and Operators Requirements {#sec-obs}

## On the Importance of Data Models {#sec-dm}

An appealing aspect about network automation techniques is that they almost apply to any kind of network. From that perspective, the functional component of a network automation framework that probably matters the most, and independent of the underlying interfaces and protocols, are the data models. Concretely, data models are instrumental in the automation of networks, service delivery, and infrastructures in general, especially that they can provide closed-loop control for adaptive and deterministic service creation, delivery, and maintenance.

Data models can be used to derive required configuration information for both network and service components, and state information that will be monitored and tracked. Likewise, they can be used during the service/network management life cycle (e.g., service instantiation, provisioning, optimization, monitoring, diagnostic, and assurance).

More than three decades of "Internet standardization" have shown that the specification of data models is not that straightforward. This is because of at least two major reasons:

*	For more than 30 years, legacy network equipment manufacturers have considered their technology as a competitive advantage, thereby leading to proprietary, vendor-specific, data models and the burden of vendor lock-ins. For example, there are more YANG proprietary modules than standarized ones. At the time of writing, {{YC}} lists 13661 unique proprietary YANG modules vs. 991 Standards modules.

*	Over the same period, operators have also developed their savoir-faire as a key competitive advantage. Such savoir-faire had to rely upon these proprietary data models (and their own ones). Operators were reluctant in the past to share their design and management practices.

The situation has changed since network "softwarization" strategies have been disclosed by vendors and operators. From a business standpoint, network "softwarization" is seen as a major transformation effort by operators, because of the flexibility and the "a la carte" approach that is promoted by "X-as-a-service" (XaaS) designs, "X" being network, platform, Network Slice {{?RFC9543}}, etc.

XaaS designs assume the availability of data models that are dynamically instantiated (along with a set of relevant policies) as a function of the "X" (and its design, for that matter). **XaaS services cannot be designed, delivered, and operated without data models.** Standard data models are thus key as they allow to:

*	Ease mapping among many (network/service) layers.
*	Ease data correlation from distinct sources.
*	Soften dependency on CLI specifics to vendors.
*	Support both top-down and bottom-up approaches for operating services:

  - Accurate control loops for adaptive and deterministic service creation, delivery, and maintenance.
  - Feed an intelligence that will drive appropriate actions to adjust the current status to align with the intended status.

OPS-REQ-STRENGTHEN-DM:
: Network softwarization can only happen with a strong, committed standardization effort, complemented by active involvement in open-source projects that facilitate access to code.
: Particularly, **without data models, a Network API is essentially useless** (see also {{sec-api}}).

## Fragmented Ecosystem {#sec-frag}

The current YANG device models ecosystem is **fragmented**: some standards data models are defined through the IETF, while similar ones are defined in other fora such as Openconfig {{OC}}.
Unlike service and network models, IETF-defined device models are not widely implemented.

OPS-REQ-DM-RATIONALIZE:
: There is a need to rationalize this space and avoid redundant efforts.

## The Network Becomes Consumable {#sec-cons}

Network connectivity can support tailored services in terms of Service Level Obejctives (SLOs), for instance, by means of Network Slice Services {{?RFC9543}}. This approach of "consuming the network" flexibly and dynamically is made possible by enabling means of exposing network capabilities to either internal or external applications. Then, network management is no longer limited to collect network status information, but it should be extended to permit the exposure of resources, capabilities, functionality, and associated information (e.g., inventory-based data).

OPS-REQ-EASE-EXPOSURE:
: Focus on protocols and data models to expose network/service capabilities, network-wide services, and related operations.

OPS-REQ-NW-API-DISCOVERY:
: Define a reference approach for service exposure discovery (APIs discovery).

## Network APIfication {#sec-api}

APIs are getting momentum as means of interworking between parties, also at the time of providing network services. As an example, {{?I-D.ietf-grow-peering-api}} defines an API for dynamically establishing BGP interconnection sessions between Autonomous Systems of different administrative domains. That same objective is also covered by the YANG data model defined in {{?RFC9834}} as exemplified in its Appendix A.10. Tools such as YANG/OpenAPI transforms are key to leverage existing data models and allow for better integration and mapping to actual realization models.

OPS-REQ-DM2API:
: Readily available API specifications should be generalized from YANG modules for fast development, prototyping, and validation.

## Lack of Profiling {#sec-pro}

Many NETCONF-related features are (being) specified by the IETF, but these features are not widely supported (e.g., YANG-Push {{?RFC8639}}). Some of these are not implemented because of the unbalance between actual operational need vs. complexity.

OPS-REQ-GUIDE-AND-PROFILE:
: The target application/applicability of a network management approach should be documented (e.g., edit profile documents that outline a set of recommendations for core/key features, along with appropriate justifications, will help foster more implementations that meet operators’ needs). This also covers security management aspects of network management. Additionaly, consider independent compliance suites to validate functions/features/etc.

OPS-REQ-ARCH:
: Need to promote more architecture and framework documents to exemplify the intended use.

> Examples of such profile documents are the various RFCs that were published by the Behavior Engineering for Hindrance Avoidance (behave) WG {{?BCP127}}.
> Another approach is to consider a model similar to the "Roadmap for Transmission Control Protocol (TCP) Specification Documents" {{?RFC7414}}.
> Such a document would serve as a guide and reference for implementers and others seeking information on 'NETCONF/RESTCONF/YANG'-related RFCs.

OPS-REQ-REASSESS:
: Additionally, reassessing the value of some IETF proposals compared to competing or emerging solutions (e.g., gRPC vs. YANG-Push) would be beneficial.

## Lack of Agile Process for (The Maintenance of) YANG Modules {#sec-agile}

RFCs might not be suited for documenting YANG modules (it takes much too long, especiallly for updates). In the meantime, there is a need for reference data models and "sufficiently stable data models".

An hybrid approach might be investigated for documenting IETF-endorsed YANG modules, such as considering an RFC to describe the initial module sketch and objectives and an official IETF repository for maintaining intermediate YANG versions.

By drawing a parallel between YANG data models and the concept of ontology used in the field of Semantic Web, the topic of YANG module maintenance could greatly benefit from proven methodologies in knowledge engineering such as {{LOT2019}} and automatic documentation tools like {{Widoco2017}}.

OPS-REQ-QUICK-BUT-WELL:
: Develop a more agile process for the development and maintenance of YANG modules in the IETF. RFCs might not be suited for documenting YANG modules.

## Integration Complexity {#sec-int}

One of the requirements listed in {{Section 3 of !RFC3535}} is the ease of use which, according to {{Section 3.2 of ?RFC6244}}, is claimed to be addressed by NETCONF and YANG. For configuration this holds true, for network observability it is unfortunately not yet. This has been confirmed with a set of network operators asking how long it takes from subscribing YANG data to make it accessible to the operator. Minutes, Hours, Days, or Weeks. None of them answered Minutes or Hours. All of them responded Days or Weeks. Hinting manual post processing of YANG data.

Collecting YANG metrics from networks is already a struggle due to late arrival of {{?RFC8639}}, {{?RFC8640}}, {{?RFC8641}}, {{?I-D.ietf-netconf-https-notif}}, and {{?I-D.ietf-netconf-udp-notif}} for configured subscription transport protocols which defined YANG-Push in the industry. This caused network vendors to implement alternative solutions to collect real-time streaming data in the meanwhile, such as gNMI which was proposed in 2018 in {{?I-D.openconfig-rtgwg-gnmi-spec}} to the IETF but not followed up on. Unfortunately, these implementations differ between network Operating Systems (OSes) due to the lack of standardization, specifically for the metadata which would ensure machine readability.

When a set of network operators where asked to where operational YANG data needs to be integrated to, the answer homogeneously was Apache Kafka Message Broker and Time Series Databases. There is a need to specify how YANG-Push can be integrated into Apache Kafka and references needed YANG-Push extensions and YANG schema registry development. The YANG-Push extensions addressing needs to make YANG-Push messages machine readable and against semantic validate able to ensure a consistent data processing.

Another challenge is that the subscribed YANG data referenced with 'datastore-subtree-filter' or 'datastore-xpath-filter' breaks semantic integrity which needs to be addressed by either updating {{Section 4 of ?RFC8641}} or proposing a new YANG module being used at the YANG-Push receiver.

OPS-REQ-INTEGRATION:
: Consider approaches to ease integration by-design (e.g., protocols and data models).

OPS-REQ-ITERATE:
: Need a velocity and approach to standardization that allows for business goals to be incrementally realized.

## YANG-formatted Data Manipulation {#sec-dama}

The use of a flat tree hierarchy in YANG data models may induce some performance issues compared to other graph models.
This can be the case, for example, during a path calculation on a network topology.
Different approaches using graph theory and compatible with YANG are currently available, but require further experimentation to generalize their adoption.
For instance, OpenDaylight {{ODL}} implements an in-memory connected graph version of YANG-based data to enable fast breadth-first search (BFS).

OPS-REQ-Y2KG:
: Need for a reference specification to translate YANG-based data into the knowledge graph (KG).

For example, {{?I-D.marcas-nmop-knowledge-graph-yang}} and {{?I-D.tailhardat-nmop-incident-management-noria}} discuss YANG-2-KG proposals to leverage automated reasoning and graph traversal techniques.

OPS-REQ-SCALE:
: Consider approaches for YANG data models to scale.

## Translation and Mapping Between Service/Network and Device Models {#sec-map}

Navigating among multiple levels of the hierarchy (service, network, device) relies
currently on proprietary solutions to graft and translate between two layers. There
is no programmatic approach to ensure lossless mappings.

OPS-REQ-LOSSLESS:
: Consider programmatic approaches to ensure lossless mappings between service/network/device data models. Means to detect, characterize, and expose loss may be considered. Note that lossless mapping is an enabler for support of deterministic verification, auditing, and tracing back along layers/models.

## (In)Consistent Data Structures in Network Protocols for Data Export {#sec-con}

Network Telemetry, as described in {{?RFC9232}}, involve a set of protocols. Due to the different requirements, one Network Telemetry protocol doesn't address all needs. This is mainly due to the nature of the subscribed data. BGP Monitoring Protocol (BMP) {{?RFC7854}} adds monitoring and tracing capabilities natively to the BGP process to minimize the processing overhead. While IPFIX {{?RFC7011}}{{?RFC7012}} can be applied according to {{?RFC5472}} to gain visibility into the data and forwarding planes, due to the amount of data, sampling as defined in {{?RFC5476}} and applied to IPFIX in {{?RFC5477}} and aggregation as defined in {{?RFC7015}} for IPFIX is needed to reduce the amount of exposed data. While YANG-Push focuses on exposing already YANG modelled data, which eases the correlation among network configuration and operational data.

{{?RFC9232}} is an informational document and does not specify what these Network Telemetry protocols should have in common to ensure consistent data structures for data export. While data types are fairly good aligned, a lack of metadata standardization among the Network Telemetry protocols is observed. In particular describing from where the metrics has been exported from and timestamping. In {{Section 4.2 of ?RFC7854}} timestamps are optional and sysName {{?RFC1213}} is only carried in the BMP initiation message ({{Section 4.3 of ?RFC7854}}), while the message header of IPFIX defined in {{Section 4.3 of ?RFC7011}} lacks the 'sysName' definition.

The lack of information from where the data is being pushed from is only known to the Network Telemetry data collection due to the transport session being established from the network node exporting the information. When Network Telemetry messages are being transformed and forwarded, this information is being lost. Therefore, it is common among network operators to augment 'sysName' and other metadata at the data collection.

The same common principle applies to when observation timestamping is missing in the Network Telemetry message. Since the data collection is the closest element to the network, a time stamp is added to give the network operator at least the information when the Network Telemetry message was collected. However, since Network Telemetry addresses real-time streaming needs, this is often not accurate enough for data correlation.

OPS-REQ-REUSABILITY:
: Consider approach to ensure reuse/consistent data structure.

## Proprietary YANG Modules, CLI, and Limited Abstraction {#sec-limit}

Leveraging on pluggins, propietary YANG data models or even CLI is still the rule in many operations, sometimes forced by the need of operating legacy infrastructures.

The complexity of developing and maintaining these means of operation is huge, as it is required to to cover many OSes and vendors along the lifetime of the network device.

Network models for the realization of services provide some "level" of abstraction and then allows for for more automation.

## Distinct Networks, Distinct Management Requirements {#sec-distinct}

From the time {{!RFC3535}} was released up to now, new kind of services and applications have been developed and deployed over the time, with very diverse, and some times contradicting, requirements. Those services have been engineered on top of multi-service networks for the sake of efficiency and simplicity, accommodating such a variety of needs. As a result, services requiring mobility, data replication, large capacity, adaptability, multi-path support, determinism, etc., coexist on the same shared network, needing from it mechanisms for graceful operation.

Likewise, such diversity of services also require different management capabilities. For example, session continuity, distribution trees, traffic engineering, congestion status notification, reordering, or on-time delivery impose very different management needs to be satisfied.

This reality is different from the one existing at the time of {{?RFC3535}}, and as such, the new identified needs can require from novel approaches to guarantee the aforementioned co-existence of services. Some networks have specific network management requirements such as the need for asynchronous operations or constraints on data compactness. An example of such networks is Delay-Tolerant Networking (DTN) {{?RFC838}} or DetNet {{?RFC8557}}.

OPS-REQ-NEW-NEED:
: Profiling main network management technologies (e.g., recommend customized transport parameters such as timeouts and transport services) is recommended than defining network management technologies that are applicable to a single deployment context.

## Implications of External Dependency {#sec-dep}

Networks are being updated to abandon the silo approach from the past towards an increasing convergence. Specifically, there are trends towards a tighter interaction and integration of different technologies previously considered as totally separated from an operational perspective. Examples of that trends are the IP and Optical integration (e.g., the introduction of colored interfaces on routers), or the extension of deterministic-behavior features to Layer 3 networks. This kind of convergence in most cases creates dependencies on the conventional network management features, which require to incorporate or integrate functionality from other technological domains.

Such convergence is also reflected on the need of interacting and interworking with distinct network parts participating in the end-to-end service delivery. Mobile access, fixed access, data center, enterprise, radio functional split (i.e., fronthaul and midhaul), neutral exchanges, intensive data networks (e.g., scientific academic networks), content distribution, etc., represent network parts constituent of end-to-end services that can impose dependencies of the management of an intermediate network.

OPS-REQ-UNSILO:
: The convergence observed in recent years also implies the need for an up-to-date refresh of management capabilities and tools for conventional networks.
: It highlights the necessity to handle the heterogeneity of data, configuration, and network management/requirements.
: From a YANG perspective, this involves easily mapping and relating the data models used to manage each specific segment.
: Resolving such issue could draw on insights from parallel technical fields such as knowledge engineering practices and concepts associated with Linked Data in the Semantic Web, areas where it is common to manage problems of heterogeneity and data reconciliation across various application domains.

## Too Much Time Between Publication of New Networking Functionality and the Associated YANG {#sec-pub}

For example, {{?RFC8667}} (IS-IS extensions for SR) was published in December 2019, while {{?I-D.ietf-isis-sr-yang}} will be published ~5 years after. There are cases where modules are not published after more than a decade of WG adoption (e.g., {{?I-D.ietf-idr-bgp-model}}).

OPS-REQ-TIMELY-DM:
: Consider having YANG as part of the protocol specification/change where possible, or have the YANG document progress in parallel.
That may slow down the protocol specification, though.

## Lack of Implementation of Proposed Solutions {#sec-impl}

New solutions proposed by WGs such as NETMOD and NETCONF very often lack an implementation or only have a partial implementation. The situation has improved with the last hackathons (e.g., for YANG-Push), but these solutions became RFCs without a known implementation:

* YANG-Push {{?RFC8641}}
* Schema-mount {{?RFC8528}}
* NMDA {{?RFC8342}}

Schema-mount allegedly has only one known implementation because of the complexity of the solution. That means the IETF most likely spent lots of cycles for something which won't be deployed ever.

While hackathons have improved the situation, the availablability of implementations is concerning. For open-source, 'sysrepo'/'libyang' are decent choices.

OPS-REQ-READILY-IMPLEM:
: The availablability of implementations is concerning. Consider catalyst approaches to trigger more (open) implementations, especially during the development of protocols/extensions.

## Tooling & Skills

### Integration with "native" IT Tooling {#sec-it}

OPS-REQ-IT-INTEGRATION:
: There is a need to ease the integration of low-level/network-oriented solution with native "IT tooling" (e.g., "https://opentelemetry.io/").

### IETF Support for Better YANG Integration {#sec-ietf-in}

OPS-REQ-IETF-TOOLS
: Ease exposure of libraries and host tools (e.g., `yangkit`) to ease integration.

### Open-source Tools {#sec-client}

While there are open-source implementations for NETCONF (e.g., NETOPEER), the gRPC/gNMI suite seems to have more support for tools on the client side.
For example, "ygot" generates structures from YANG models and these can easily be used by a client to configure a device with gNMI. NETCONF is not supported though (the XML tags are needed).

OPS-REQ-CLIENT-TOOLS:
: Focus on tooling is needed, especially on the client side.

### Skills {#sec-skills}

The IETF is not the expert community in data engineering. The experts are in the data industry. Without them, integration in data processing chains like Data Mesh is going to be a challenge.

OPS-REQ-BRIDGE:
: Create an eco-system where data and networking engineers can collaborate.

## New Service Approaches {#sec-new}

The virtualization trend have made posible to dynamically instantiate Service Functions (SFs) in distributed compute facilities in the form of virtual machines or containers, as micro-services. The instantiation of the SFs is governed by cloud management systems, as it is the connectivity among the different instances or micro-services. That connectivity is typically realized by using overlay mechanisms, without any further interaction with the network. However, this appraoch seems to be insuficient for future services demanding stringent requirements in terms of SLOs.

OPS-REQ-GLUE:
: The distinct approaches followed in both the compute and the network environments makes necessary to define suitable mechanisms for enabling an efficient interplay, while highly automating the overall service delivery procedure.

## Many Solutions for the Same Problem, but Lack of Clear Applicably Guidance {#sec-guid}

There are several solutions that were standardized for network management purposes. For example, management of ACLs by means to BGP FlowSpec {{?RFC8955}}{{?RFC8956}} or  by means of NETCONF/YANG {{?RFC8519}}. There is no cross referencing between the two standards or delimits its applicability scope vs the other approach.

Likewise, BGP FlowSpec did not reuse the IPFIX Information Elements.

OPS-REQ-GUIDANCE:
: The target application/applicability of a network management approach should be integrated in the specification itself.

# Updated Operators' Requirements

## Summary {#sec-reqs}

OPS-REQ-STRENGTHEN-DM:
: Network softwarization can only happen with a strong, committed standardization effort, complemented by active involvement in open-source
projects that facilitate access to code.

OPS-REQ-DM-RATIONALIZE:
: Rationalize this space and avoid redundant efforts (in almost all layers (IP, optic, etc.)). Unlike service and network models, Standard-based device models are not widely implemented.

OPS-REQ-EASE-EXPOSURE:
: Focus on protocols and data models to expose network/service capabilities, network-wide services, and related operations.

OPS-REQ-NW-API-DISCOVERY:
: Define a reference approach/process for service exposure discovery (APIs discovery).

OPS-REQ-DM2API:
: Readily available API specifications should be generalized from YANG modules for fast development, prototyping, and validation.

OPS-REQ-GUIDE-AND-PROFILE:
: The target application/applicability of a network management approach should be documented (e.g., edit profile documents that outline a set of recommendations for core/key features, along with appropriate justifications, will help foster more implementations that meet operators’ needs). This also covers security management aspects of network management. Additionaly, consider independent compliance suites to validate functions/features/etc.

OPS-REQ-ARCH:
: Need to promote more architecture and framework documents to exemplify the intended use.

OPS-REQ-REASSESS:
: Reassess the value of some IETF proposals, including compared to competing or emerging solutions (e.g., gNMI).

OPS-REQ-QUICK-BUT-WELL:
: Develop a more agile process for the development and maintenance of YANG modules in the IETF. RFCs might not be suited for documenting YANG modules.

OPS-REQ-INTEGRATION:
: Consider approaches to ease integration by-design (e.g., protocols and data models). The integration covers both horizontal and vertical realms. For example, there is a lack of enablement of this integration across standard bodies that operators are left to solve.

OPS-REQ-ITERATE:
: Need a velocity and approach to standardization that allows for business goals to be incrementally realized.

OPS-REQ-Y2KG:
: Need for reference specifications to translate YANG-based data into the knowledge graph. Sample use cases to illustrate the intended use should be considered as well.

OPS-REQ-SCALE:
: Consider approaches for YANG data models to scale, including protocol considerations (transactions, etc.). Specifically, address telemetry scalability enhancements.

OPS-REQ-LOSSLESS:
: Consider programmatic approaches to ensure lossless mappings between service/network/device data models. Means to detect, characterize, and expose loss may be considered. Note that lossless mapping is an enabler for support of deterministic verification, auditing, and tracing back along layers/models.

OPS-REQ-REUSABILITY:
: Consider approaches to ensure reuse/consistent data structure across various network management segments. This will ease correlating data learned using different means (IPFIX {{?RFC7011}},  BGP Monitoring Protocol (BMP) {{?RFC7854}}, SYSLOG {{?RFC5424}}, etc.).

OPS-REQ-NEW-NEED:
: Profiling main network management technologies (e.g., recommend customized transport parameters such as timeouts and transport services) is recommended than defining network management technologies that are applicable to a single deployment context.

OPS-REQ-UNSILO:
: Necessity to handle the heterogeneity of data, configuration, and network management/requirements. Resolving such issue could draw on insights from parallel technical fields such as knowledge engineering practices and concepts associated with Linked Data in the Semantic Web, areas where it is common to manage problems of heterogeneity and data reconciliation across various application domains.

OPS-REQ-TIMELY-DM:
: Consider having YANG as part of the protocol specification/change where possible, or have the YANG document progress in parallel.

OPS-REQ-READILY-IMPLEM:
: The availability of implementation is concerning. Consider catalyst approaches to trigger more (open) implementations, especially during the development of protocols/extensions.

OPS-REQ-IT-INTEGRATION:
: There is a need to ease the integration of low-level/network-oriented solution with native "IT tooling" (e.g., https://opentelemetry.io/).

OPS-REQ-IETF-TOOLS:
: Ease exposure of libraries and host tools (e.g., yangkit) to ease integration.

OPS-REQ-CLIENT-TOOLS:
: Focus on tooling is needed, especially on the client side. There is a need for tools that are easy to use. Likewise, there is need for support for multiple friendly, stable, and feature-rich libraries for programming languages.

OPS-REQ-BRIDGE:
: Create an eco-system where data and networking engineers can collaborate.

OPS-REQ-GLUE:
: Distinct approaches followed in both the compute and the network environments make necessary to define suitable mechanisms for enabling an efficient interplay, while highly automating the overall service delivery procedure.

OPS-REQ-GUIDANCE:
: The target application/applicability of a network management approach should be integrated in the specification itself.

## Categorization

{{table-req-cat}} provides a classification of the requirements listed in {{sec-reqs}}. It specifically tag whether a requirement:

* Belongs to data modeling (DM)
* Requires protocol work (Protocol)
* Impacts deployability of standardized approaches (Deployability)
* Has implications on integration effort by operators (Integration)
* Requires some adaptations to a Standards Developing Organization (SDO) process (SDO Process)
* Allows better coordination (Collaboration & Cooperation)
* Is relevant to skills transformations (Skills)

|Ops Requirement Label   | DM  | Protocol | Deployability  | Integration    |SDO Process| Collaboration & Cooperation  | Skills         |
|------------------------|:---:|:--------:|:--------------:|:--------------:|:---------:|:----------------------------:|:--------------:|
|OPS-REQ-STRENGTHEN-DM   |	X   |	          |      X		   |	              |           |	                           |                |
|OPS-REQ-DM-RATIONALIZE  |	X   |          |      X 		   |                |    X      |            X                 |                |
|OPS-REQ-EASE-EXPOSURE   |	X   |     X    |      X		   |      X         |           |            	               |                |
|OPS-REQ-NW-API-DISCOVERY|	    |          |      X		   |      X         |           |            	               |                |
|OPS-REQ-DM2API          |	    |          |      X		   |                |           |            	               |                |
|OPS-REQ-GUIDE-PROFILE   |	X   |     X    |      X		   |                |           |            	               |                |
|OPS-REQ-ARCH            |     |     X    |      X		   |                |           |            	               |                |
|OPS-REQ-REASSESS        |	    |     X    |       		   |                |           |            	               |                |
|OPS-REQ-QUICK-BUT-WELL  |	X   |     X    |      X		   |                |           |            	               |                |	
|OPS-REQ-INTEGRATION     |     |          |      X		   |      X         |    X      |            	               |                |			
|OPS-REQ-ITERATE         |	    |          |       		   |                |    X      |            X                 |                |		
|OPS-REQ-Y2KG            |	    |          |      X		   |      X         |           |            	               |                |
|OPS-REQ-SCALE           |	X   |      X   |       		   |                |           |            	               |                |
|OPS-REQ-LOSSLESS        |	    |          |      X		   |      X         |    X      |            	               |                |
|OPS-REQ-REUSABILITY     |	    |      X   |       		   |      X         |    X      |            	               |                |
|OPS-REQ-NEW-NEED        |	    |      X   |       		   |                |           |            	               |                |
|OPS-REQ-UNSILO          |	    |          |      X		   |      X         |           |            	               |                |	
|OPS-REQ-TIMELY-DM       |	X   |          |      X		   |                |           |            	               |                |		
|OPS-REQ-READILY-IMPLEM  |	X   |     X    |      X		   |                |    X      |            	               |                |	
|OPS-REQ-IT-INTEGRATION  |	    |          |      X		   |      X         |           |            	               |                |	
|OPS-REQ-IETF-TOOLS      |	    |          |       		   |                |    X      |            	               |        X       |
|OPS-REQ-CLIENT-TOOLS    |	    |          |      X		   |      X         |           |            	               |        X       |	
|OPS-REQ-BRIDGE          |	    |          |       		   |                |           |            X                 |      X         |
|OPS-REQ-GLUE            |	    |          |       		   |      X         |           |            	               |        X       |
|OPS-REQ- GUIDANCE       |	    |          |      X  		   |                |           |            	               |                |
{: #table-req-cat title='Requirements Classification'}

## Overall New Requirements Levels: Operators View

{{table-ops-view}} provides the requirement level of {{sec-reqs}} from an operator perspective.

|Ops Requirement Label    | Overall Level  |
|------------------------:|:--------------:|
|OPS-REQ-STRENGTHEN-DM    |    Strong      |
|OPS-REQ-DM-RATIONALIZE   |    Strong      |
|OPS-REQ-EASE-EXPOSURE    |    Strong      |
|OPS-REQ-NW-API-DISCOVERY |  Nice to have  |
|OPS-REQ-DM2API           |    Strong      |
|OPS-REQ-GUIDE-AND-PROFILE|  Nice to have  |
|OPS-REQ-ARCH             |    Strong      |
|OPS-REQ-REASSESS         |    Strong      |
|OPS-REQ-QUICK-BUT-WELL   |    Strong      |
|OPS-REQ-INTEGRATION      |    Strong      |
|OPS-REQ-ITERATE          |    Strong      |
|OPS-REQ-Y2KG             |  Nice to have  |
|OPS-REQ-SCALE            |    Strong      |
|OPS-REQ-LOSSLESS         |  Nice to have  |
|OPS-REQ-REUSABILITY      |    Strong      |
|OPS-REQ-NEW-NEED         |  Nice to have  |
|OPS-REQ-UNSILO           |    Strong      |
|OPS-REQ-TIMELY-DM        |    Strong      |
|OPS-REQ-READILY-IMPLEM   |    Strong      |
|OPS-REQ-IT-INTEGRATION   |  Nice to have  |
|OPS-REQ-IETF-TOOLS       |  Nice to have  |
|OPS-REQ-CLIENT-TOOLS     |    Strong      |
|OPS-REQ-BRIDGE           |    Strong      |
|OPS-REQ-GLUE             |  Nice to have  |
|OPS-REQ-GUIDANCE         |  Nice to have  |
{: #table-ops-view title='Operators Requirements Levels'}


## Consolidated Requirements

This section provides a consolidated view of main requirements that takes into account inputs from actors beyond operators:

* Put more focus on service and network data models (OPS-REQ-EASE-EXPOSURE, OPS-REQ-STRENGTHEN-DM) while ensuring that the realization of these abstractions
  can be easily correlated with underlying functionalities (OPS-REQ-INTEGRATION).
* Progress much faster (OPS-REQ-QUICK-BUT-WELL, OPS-REQ-TIMELY-DM).
* Implement minimal functionality, not bells and whistles (OPS-REQ-ITERATE).
* Have running code while a specification is under development (OPS-REQ-READILY-IMPLEM, OPS-REQ-TOOLS).
* Have vendors and operators on board at the time of developing a network management solution.
* Provide independent compliance suites to validate features (OPS-REQ-GUIDE-AND-PROFILE).
* Need for means to correlate data learned from different means (OPS-REQ-REUSABILITY).
* Investigate approaches to ease adoption and integration into an operator’s environments (OPS-REQ-EASE-EXPOSURE, OPS-REQ-DM2API, OPS-REQ-INTEGRATION).
* Network-centric approaches have limits, need to better integrate and learn from techniques in other domains (OPS-REQ-BRIDGE).

# Security Considerations

This document does not define any protocol or architecture.

# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}

Thanks to Christian Jacquenet and Jean-Michel Combes for their inputs.

Thanks to Benoît Claise and Alex Clemm for the comments.

Many of the requirements were extracted from contributions to the IAB Next Era of Network Management Operations (NEMOPS) Workshop {{?I-D.iab-nemops-workshop-report}}.

Thanks to Ian Farrer, Brad Peters, Chongfeng Xie, and Qin Wu for their contribution to consolidate the requirements.
