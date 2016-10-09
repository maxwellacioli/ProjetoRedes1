---
title: SNMP Improviment
abbrev: 
date: 2016
category: info
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
 -
    name: Maxwell Acioli, Rubens Pessoa
    organization: Federal University Alagoas

normative:
  RFC2119:

informative:

--- abstract

It is an application layer protocol widely used in network management systems to facilitate the exchange of management information between different devices connected to the network. This paper proposes an improvement in the protocol, in order to avoid sending a large volume of information in a specific application of the protocol.

--- middle

# Introduction

One of the weaknesses SNMP protocol is the transmission of a large volume of unnecessary information to the manager when it makes a request for specific information to the agent. This document presents a proposal that serves as an alternative to contonar the mentioned weakness.
In the first section will present a brief description of the SNMP protocol. Then, in section two the SNMP commands are described. In Section three discussed the standard protocol procedure. Section four will address the SNMP protocol weaknesses. The last section will bring the proposal for improving the SNMP protocol.

## Terminology

In this document, the key words "MUST", "MUST NOT", "REQUIRED",
"SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY",
and "OPTIONAL" are to be interpreted as described in BCP 14, RFC 2119
{{RFC2119}}.

# Description

## Master Manager

## Agent

## MIB

# Protocol Commands

