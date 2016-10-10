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
  RFC1213:

informative:

--- abstract

It is an application layer protocol widely used in network management systems to facilitate the exchange of management information between different devices connected to the network. This paper proposes an improvement in the protocol, in order to avoid sending a large volume of information in a specific application of the protocol.

--- middle

# Introduction

One of the weaknesses SNMP protocol {{RFC1157}} is the transmission of a large volume of unnecessary information to the manager when it makes a request for specific information to the agent. This information is in the MIB {{RFC1066}} as part of the agent's responses. This document presents a proposal that serves as an alternative to contonar the mentioned weakness.
In the first section will present a brief description of the SNMP protocol. Then, in section two the SNMP commands are described. In Section three discussed the standard protocol procedure. Section four will address the SNMP protocol weaknesses. The last section will bring the proposal for improving the SNMP protocol.

# Description

## Manager

The manager stays on the network servers. Its main rule is to request and receive from the agents necessary informations to manage the network. 

## Agent

The agent is present on each node of the network managed by SNMP. It’s important to notice that an agent is not necessarily a computer. Any device connected to the network with support to SNMP will behave like an agent.

## MIB

MSI (Structure of Management Information) is a method for defining managed objects and their respective managements. It is a set of objects contained in a device management information.
MIB-II {{RFC1213}} is a specific MIB. Its main objective is to provide specific information about the managed device via TCP / IP. Proprietary MIBs are developed by manufacturers of devices because through them it is possible that a manufacturer add specific information to your devices.

# Protocol Commands


The SNMP doesn’t have a lot of commands. These commands must indicate the name (which is unique for each object) of the object. 

1. GET - Sent by the manager to a managed device. It aims to retrieve one or more values from the managed device.
2. GETNEXT - Retrieves the value of the next OID in the MIB tree.
3. GETBULK - Used to retrieve voluminous data form large MIB table.
4. SET - Modify or assign the value of the managed device.
5. INFORM - This command is similar to the TRAP command. It includes confirmation from the SNMP manager on receiving the message.
6. TRAP - This command is initialized by the Agent, unlike the GET’s and SET’s. It announces the occurrence of an event in the managed device to the manager.
7. RESPONSE - It is the command used to carry back the value(s) or signal of actions directed by the SNMP Manager.

# Standard Procedures
SNMP works as a simple operating model, called model "fetch-store" or "read-write model." Uses UDP protocol (port 161) to send and
receiving requests, manager receives TRAPS in port 162(UDP).
Messages Format:
Resquest: snmpget -v2c -c public 192.168.254.1 sysUpTimeInstance
Response: DISMAIN-EVENT-MIB::sysUpTimeInstance = Timesticks: (355815) 0:59:18.15


# SNMP Weakness

# Proposal

