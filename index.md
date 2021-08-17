## Introduction

This project started as a [Fund 5 Catalyst Proposal for the Cardano Blockchain](https://cardano.ideascale.com/a/dtd/Oracle-Performance-Metrics/352231-48088 "Google's Homepage").

Our goal was to periodically store performance metadata that has been appropriately signed for authenticity and provide a tool for aggregating this data.

This document finalises all pledged deliverables for that funded proposal and also poses unsolved questions and future work for the project.

## Croesus?

Pronounces (KREE-sus), this project derives its name from the King of Lydia, who - as told by Herodutus [tested the oracles of his time.](https://en.wikipedia.org/wiki/Croesus#Croesus'_votive_offerings_to_Delphi)

## Define generic assessment criteria for automated services

Our initial thoughts were to extend the schema.org [SolveMathAction])https://schema.org/SolveMathAction) and [MathSolver](https://schema.org/MathSolver) schemas to create a standards-based structure for registration and assessment of automated services.

During our early Proofs-of-Concept, it became apparent that these schemas were too verbose, and fell short on being able to support further work we have for this protocol. Therefore, we narrowed the focus down to two different types of reporting elements for the protocol. Registration and Reporting.

This approach already has some precedent in the Cardano community. https://nut.link/, the first generation Cardano Oracle registry uses the approach for Oracles themselves.

### Registration

In order to start reporting on oracle utility, they must first be registered. The address which registers the oracle is able to post authoritative reports, highlighted by the Croesus reporting tool.

Oracles, or any other service (such as a Machine Learning model) can be registered using either onchain, or offchain data, but must be accompanied by verifiable data to validate the reported metrics.

The service itself can be public (via an API), offline or protected (via a API which requires credentials), but the verifiable data must be publicly accessible. Examples of storage places for data are Cloud Storage buckets, IPFS, GitHub repositories or on a website.

#### Example



Schema

### Reporting

#### Reporting Validation

A natural consequence of making datasets freely available is that they can be repurposed or used as validation datasets for new services.

## What is the incentive for a service owner to create processes which report on metadata?

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
