
Simple Network Management Protocol

# Manager

# Agent

# MIB

A MIB is data base that defines to the SNMP manager what the monitored device can report and what parameters is has. It can be compiled (binary?) and added to the SNMP manager

# Supervision Methods

## Traps

This is the old method of supervision, where the Agent sends a trap to the manager in case of an issue. This is not really helpful since the Agent maybe offline and nothing will be flaged.

- Immediat

## Polling

In this method the Manager asks the Agent periodically for statistics and data.


