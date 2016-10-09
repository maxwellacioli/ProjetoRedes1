---
title: Suggestion for Improvement in the SNMP Protocol
abbrev: SNMP Improviment
date: 2016
category: info
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
 -
    ins: M. E. A. Silva
    name: Maxwell Esdra Acioli Silva
    org: Federal University of Alagoas
    street: Av. Lourival Melo Mota, S/N
    city: Maceio
    country: Brazil
    phone: +55-82-3241-1401
    email: meas@ic.ufal.br
 -
    ins: R. Pessoa
    name: Rubens Pessoa
    org: Federal University of Alagoas
    street: Av. Lourival Melo Mota, S/N
    city: Maceio
    country: Brazil
    phone: +55-82-3241-1401
    email: rpbf@ic.ufal.br
    
normative:
  RFC1157:
  RFC1066:

informative:

--- abstract

It is an application layer protocol widely used in network management systems to facilitate the exchange of management information between different devices connected to the network. This paper proposes an improvement in the protocol, in order to avoid sending a large volume of information in a specific application of the protocol.

--- middle

# Introduction

One of the weaknesses SNMP protocol is the transmission of a large volume of unnecessary information to the manager when it makes a request for specific information to the agent. This document presents a proposal that serves as an alternative to contonar the mentioned weakness.
In the first section will present a brief description of the SNMP protocol. Then, in section two the SNMP commands are described. In Section three discussed the standard protocol procedure. Section four will address the SNMP protocol weaknesses. The last section will bring the proposal for improving the SNMP protocol.

# Description

## Manager

The manager stays on the network servers. Its main rule is to request and receive from the agents necessary informations to manage the network. 

## Agent

The agent is present on each node of the network managed by SNMP. It’s important to notice that an agent is not necessarily a computer. Any device connected to the network with support to SNMP will behave like an agent.

## MIB

# Protocol Commands

