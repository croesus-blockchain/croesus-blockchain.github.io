## Introduction

This project started as a [Fund 5 Catalyst Proposal for the Cardano Blockchain](https://cardano.ideascale.com/a/dtd/Oracle-Performance-Metrics/352231-48088 "Google's Homepage").

This document fulfills the final of all pledged deliverables, to report on the findings of the project.

## Define generic assessment criteria for automated services

Our initial thoughts were to extend the schema.org SolveMathAction and MathSolver schemas to create a standards-based structure for registration and assessment of automated services.

Shortly after implementation, it became apparent that these schemas were too verbose, so we narrowed the focus down to two different types of reporting elements for the protocol

### Registration

### What is the incentive for a service owner to create processes which report on metadata?

### Reporting

#### Reporting Validation

A natural consequence of making datasets freely available is that they can be repurposed or used as validation datasets for new services.

## Choose a specific application to create a proof of concept reporting tool

During development of the protocol we observed several categories of services, described below:

### Randomiser

A service which produces a random number or random outcome

Commonly used in gambling and other gaming applications, these need to be assessed based on the spread of values reported.

A service which applies a model across a dataset

An example are Machine Learning Models, such as a Credit Scoring application used to assess an entity loan. The reliability / utility of these services are usually based on specific metrics such as Gini or Kolmogorov–Smirnov (KS) test

* A service which reports a currency or token exchange rate

On-chain reporting of exchange rates can be retrospectively compared against other exchanges to create metrics such as distance from mean

* A service which verifies an event occurred

An authoritative peer reporting metric is required to confirm an event was recorded in a timely manner.

#### Auto-Disovery through Metadata

Our project stumbled upon a novel use of blockchain metdata during this research. Metadata reported through the resiliant blockchain network can be used as a native, in-built auto discovery mechanism.

Our project looks to extend this idea and dive deeper into these use cases through a proposal in Catalyst Fund 6.

## Demonstrate reporting of metadata

## Lessons Learnt

## Unsolved Questions

## Future Work
