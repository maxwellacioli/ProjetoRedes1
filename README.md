---
title: Suggestion for SNMP Improvement
abbrev: SNMP Improvement
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
    ins: R. P. de B. Filho
    name: Rubens Pessoa de Barros Filho
    org: Federal University of Alagoas
    street: Av. Lourival Melo Mota, S/N
    city: Maceio
    country: Brazil
    phone: +55-82-3241-1401
    email: rpbf@ic.ufal.br
 -
    ins: H. G. Barbosa
    name: Helivelton Gomes Barbosa
    org: Federal University of Alagoas
    street: Av. Lourival Melo Mota, S/N
    city: Maceio
    country: Brazil
    phone: +55-82-3241-1401
    email: helivelton@ic.ufal.br
 -
    ins: M. C. dos Santos
    name: Manoela Cassia dos Santos
    org: Federal University of Alagoas
    street: Av. Lourival Melo Mota, S/N
    city: Maceio
    country: Brazil
    phone: +55-82-3241-1401
    email: manoelacs@ic.ufal.br
    
normative:
  RFC1157:
  RFC1066:
  RFC1213:


informative:
  BOOK:
    title: Essential SNMP 2nd ed.
    author:
#      -
        ins: D. Mauro
        name: Douglas Mauro
    date: 2005

--- abstract

SNMP is an application layer protocol widely used in network management systems. The protocol helps to facilitate the exchange of management information between different devices connected to the network. This document proposes an improvement in SNMP in order to avoid sending a large volume of information in a specific application of the protocol.

--- middle

# Introduction

One of the weaknesses of SNMP {{RFC1157}} is the transmission of a large volume of unnecessary information to the manager when it receives a response from the agent after a request. This information is carried in MIB (Management Information Base) {{RFC1066}} as part of the agent's response. This document presents a proposal that serves as an alternative to solve the mentioned weakness.
In the first Section we present a brief description of the SNMP. Then, in Section 2 we describe SNMP commands. In Section 3 we discuss the standard protocol procedure. Section 4 addresses the SNMP weaknesses. The last Section will bring the proposal for improving the protocol.

# Description

SNMP is an application layer protocol widely used in network management systems to facilitate the exchange of management information between different devices connected to the network.
It is based on the manager / agent model.
It consists of the following components:

## Manager

The manager stays on the network servers. Its main rule is to request and receive from the agents necessary informations to manage the network. 

## Agent

The agent is present on each node of the network managed by SNMP. It is important to notice that an agent is not necessarily a computer. Any device connected to the network with support to SNMP will behave like an agent.

## MIB

MSI (Structure of Management Information) is a method to define managed objects and their respective managements. It is a set of objects contained in a device management information.
MIB-II {{RFC1213}} is a specific MIB. Its main objective is to provide information about the managed device via TCP/IP. Figure 1 shows the MIB-II structure.

~~~~~~~~~~

+-+-+-+-+-+ 
|mib-II(1)|
+-+-+-+-+-+
|  +-+-+-+-+-+ 
|--|system(1)|
|  +-+-+-+-+-+
|  +-+-+-+-+-+-+-+ 
|--|interfaces(2)|
|  +-+-+-+-+-+-+-+
|  +-+-+-+
|--|at(3)|
|  +-+-+-+
|  +-+-+-+ 
|--|ip(4)|
|  +-+-+-+
|  +-+-+-+-+ 
|--|icmp(5)|
|  +-+-+-+-+
|  +-+-+-+-+
|--|tcp(6) |
|  +-+-+-+-+
|  +-+-+-+-+
|--|udp(7) |
|  +-+-+-+-+
|  +-+-+-+-+ 
|--|egp(8) |
|  +-+-+-+-+
|  +-+-+-+-+-+-+-+-+-+ 
|--|transmission(10) |
|  +-+-+-+-+-+-+-+-+-+
|  +-+-+-+-+-+ 
|--|snmp(11) |
   +-+-+-+-+-+
   
~~~~~~~~~~
{: #mib2 title="MIB-II Structure"}

Device manufacturers can develop proprietary MIBs. This makes it possible to add specific information to their devices in MIB. 

# Protocol Commands

The SNMP does not have a lot of commands. The commands must indicate the an unique name for each object. 

1. GET - Sent by the manager to a managed device. It aims to retrieve one or more values from the managed device.
2. GETNEXT - Retrieves the value of the next OID in the MIB tree.
3. GETBULK - Used to retrieve voluminous data form large MIB table.
4. SET - Modifies or assigns the value of the managed device.
5. INFORM - This command is similar to the TRAP command. It includes confirmation from the SNMP manager on receiving the message.
6. TRAP - This command is initialized by the Agent, unlike the GET’s and SET’s. It announces the occurrence of an event in the managed device to the manager.
7. RESPONSE - It is the command used to carry back the value(s) or signal of actions directed by the SNMP Manager.

# Standard Procedures

SNMP works as a simple operating model, called "fetch-store model" or "read-write model". It uses UDP protocol (port 161) to send and receive requests. Manager receives TRAPS in port 162 via UDP.
Messages Format:
Resquest: snmpget -v2c -c public 192.168.254.1 sysUpTimeInstance
Response: DISMAIN-EVENT-MIB::sysUpTimeInstance = Timesticks: (355815) 0:59:18.15
The Figure 2 shows the TCP/IP protocol suite, which is the basis for all TCP/IP communication.

~~~~~~~~~~~~~~~~~~~~

+-+-+-+-+-+-+-+           +-+-+-+-+-+-+-+
|     NMS     |	          |    Agent    |
+-+-+-+-+-+-+-+           +-+-+-+-+-+-+-+
| Application |           | Application |
+-+-+-+-+-+-+-+           +-+-+-+-+-+-+-+
|     UDP     |           |     UDP     |
+-+-+-+-+-+-+-+           +-+-+-+-+-+-+-+
|     IP      |	          |     IP      |
+-+-+-+-+-+-+-+           +-+-+-+-+-+-+-+
|     NAP     |           |     NAP     |
+-+-+-+-+-+-+-+           +-+-+-+-+-+-+-+
|   |   |   |               |   |   |   |
|   |   |   |------(1)------|   |   |   |
|   |   |                       |   |   |
|   |   |----------(2)----------|   |   |
|   |                               |   |    
|   |--------------(3)--------------|   |
|                                       |
|-Internetwork Connecting NMS to Agent -|

(1): Trap sent to port 162 on the NMS
(2): SNMP request sent from the NMS to the agent port 161
(3): Response to SNMP request from the agent to port 161 on the NMS

~~~~~~~~~~~~~~~~~~~~
{: #model title="TCP/IP communication model and SNMP"}

# SNMP Weakness

This protocol is not appropriated for the managment of large and complex networks due to the limitation on the pooling performance (pooling is the operation performed to begin a transaction between manager and agent);

The basic SNMP standard provides only common authentication, to this problem the SNMP Research presents the ESO (Extended Security Options), an extended standard of encryption using the SNMPv3 standard technics. It defines, creates and deploys improvements to the security of the SNMPv3 architecture. Those three factors imply strong encryption, third party authentication and ignition key;

The SNMP MIB model is limitated and does not support applications that question the management, based on values or object types.

# Proposal

In this proposal, we assume that the network must have a master manager. The function of the master manager, besides requesting and receiving the agents metadata for controlling the network, is to learn the usage patterns with respect to time. After some time has passed, the master manager infers the state that must be set to a given variable based on usage history.

This intelligence must be integrated with the manager software using a reinforcement learning algorithm such as Q-learning.

But why?

Let's imagine a scenario in IoT (Internet-of-Things). Suppose someone has a home that has a server controlling all the lights in the house. In this server, there is a SNMP manager to control the status of each lamp. Each lamp has been set as a SNMP agent. With time and use, the server learns the exact time that she comes home and turns on the lights. In a certain moment, when she comes home, the server will automatically turn on the lights.

What if she changed her habits?

We propose the software developers to include a reinforcement learning algorithm in the implementation of SNMP software suite for dealing with these cases. It may take a while, but it will adapt to the user's behaviors.
