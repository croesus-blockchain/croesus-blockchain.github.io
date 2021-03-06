## Introduction

This project started as a [Fund 5 Catalyst Proposal for the Cardano Blockchain](https://cardano.ideascale.com/a/dtd/Oracle-Performance-Metrics/352231-48088 "Fund 5 Proposal").

Our goal was to periodically store performance metadata that has been appropriately signed for authenticity and provide a tool for aggregating this data.

This document finalises all pledged deliverables for that funded proposal and also poses unsolved questions and future work for the project.

The future work has helped inspire subsequent projects:
* A [Fund 6 Catalyst Proposal](https://cardano.ideascale.com/a/dtd/Applying-Oracle-Performance-Metrics/369013-48088 "Fund 6 Proposal") to extend the protocol, applying it to three distinct use cases
* A [Fund 7 Catalyst Proposal](https://cardano.ideascale.com/a/dtd/Cardano-Risk-Assessment-Tool/382089-48088 "Fund 7 Proposal") to demonstrate a real-world application in the form of a Blockchain Risk Assessment Tool

## Croesus?

Pronounced (KREE-sus), this project derives its name from the King of Lydia, who - as told by Herodutus - [tested the oracles of his time.](https://en.wikipedia.org/wiki/Croesus#Croesus'_votive_offerings_to_Delphi)

## Define generic assessment criteria for automated services

Our initial thoughts were to extend the schema.org [SolveMathAction](https://schema.org/SolveMathAction) and [MathSolver](https://schema.org/MathSolver) schemas to create a standards-based structure for registration and assessment of automated services.

During our early Proofs-of-Concept, it became apparent that these schemas were too verbose, and fell short on being able to support further work we have for this protocol. Therefore, we narrowed the focus down to two different types of reporting elements for the protocol. Registration and Reporting.

This approach already has some precedent in the Cardano community. [nut.link](https://nut.link/), the first generation Cardano Oracle registry uses the approach for Oracles themselves.

### Registration

In order to start reporting on oracle utility, they must first be registered. The address which registers the oracle is able to post authoritative reports, highlighted by the Croesus reporting tool.

Oracles, or any other service (such as a Machine Learning model) can be registered using either onchain, or offchain data, but must be accompanied by verifiable data to validate the reported metrics.

The service itself can be public (via an API), offline or protected (via a API which requires credentials), but the verifiable data must be publicly accessible. Examples of storage places for data are Cloud Storage buckets, IPFS, GitHub repositories or on a website.

The metrics reported can be either integer or floating point numbers.

#### Example

```json
{
  "11445640693": {
      "protocol": "croesus_registration_v1",
      "name": "Registration Name",
      "description": [
          "Description of the registration. Note the limit of 64 bytes per ",
          "line. All 'description' and 'url' fields can be string arrays or",
          "regular strings."
      ],
      "type": "offchain",
      "metrics": [
          {
              "name": "number",
              "value": "24",
              "type": "integer",
              "description": "Integers are supported"
          },
          {
              "name": "pi",
              "value": "3.14159265",
              "type": "float",
              "description": [
                  "Floats are supported too."
              ]
          }
      ],
      "endpoint": {
          "type": "public",
          "url": [
              "https://www.croesus-blockchain.com/randomiser-true?seed=",
              "103841014"
          ]
      },
      "documentation": {
          "url": "https://www.croesus-blockchain.com/"
      },
      "tags": [
          "random",
          "number",
          "generation"
      ],
      "validation": {
          "url": "https://croesus-blockchain.github.io/random_true_001.txt"
      },
      "reference": [
          "(Optional) field used to link with another registration txid.",
          "Multiple transaction ids (from registrations or reports)",
          "can be referenced here for super-set validation use-cases",
          "such as those used for Machine Learning"
      ]
  }
}
```

Example on Cardano Testnet)

https://explorer.cardano-testnet.iohkdev.io/en/transaction.html?id=496ad2e3939830fa31ddcea895199a779f4e243492b0783593793116ddeb223d

Meta data is lodged using the transaction meta data label: "11445640693", which is "CROESUS" in Base31

The "reference" field can be used to link to another Croesus registration. Its purpose is to create new versions of services, or for Machine Learning use cases where the results and data from one service can be used to build another.

### Reporting

The registration element only established the first data element in the reporting history of our Oracle. In order to create a time series of data points, we should regularly publish reports.

Reports submitted by the same address as the registration are considered authoritative.

The reference is the transaction hash of the registration.

The metrics are updated values to the targets referened in the registration.

Reports allow for updates of outcome tags associated with a service.

Validation contains the publicly accessible file used to determine the aggregate metrics.

```json
{
  "11445640693": {
      "protocol": "croesus_report_v1",
      "reference": "baa8ced1cfcad8ab96b84c3133007d2f832c2498dfcc7db83c5e9e7d46f5687b",
      "note": [
          "A report can be accompanied by an optional explanatory note",
          "useful to add additional context to any metrics reported",
          "for this period. Note that the same set of metrics",
          "used for registrations should be present in each report"
      ],
      "tags": [
          "Additional",
          "Optional",
          "Tags",
          "Can",
          "Be",
          "Provided",
          "Each",
          "Report"
      ],
      "validation": {
          "url": [
              "https://really-long-urls-can-be/broken-up?over=64&byte=string&ar",
              "rays=1&otherwise=just&use=a&regular=string"
          ],
          "description": [
              "Some explanatory notes can be provided with the",
              "validation url, which should be publicly accessible.",
              "Croesus Reporting tools should note validations that",
              "have broken links"
          ]
      },
      "metrics": [
          {
              "name": "number",
              "value": "100000"
          },
          {
              "name": "pi",
              "value": "3.14159265"
          }
      ]
  }
}
```

Example on Cardano Testnet)

https://explorer.cardano-testnet.iohkdev.io/en/transaction?id=b1c49a5acb9d45d8347c96527c7ee89890290aff5e85f263f323da8ffb58e4c0

Like registrations, metadata reports are lodged using the transaction meta data label: "11445640693", which is "CROESUS" in Base31

#### Reporting Validation

A natural consequence of making datasets freely available is that they can be repurposed or used as validation datasets for new services.

So called "Superset Validations" can be leveraged for Distributed Machine Learning use cases, but appear as as a report element in the protocol.

## What is the incentive for a service owner to create processes which report on metadata?

The maintainer of the oracle, or the community running an oracle pool have an incentive to inform users and the ecosystem how well their Oracle performs compared to their competitors.

Formalising the reporting mechanism allows the community to build reporting toolsets using the data creating a competitive marketplace for Oracle Services.

Storing the data on the blockchain allows for in-built auto-discovery of players in this marketplace, and the effectiveness of Oracles using verifiable metrics they are contributing.

## Choose a specific application to create a proof of concept reporting tool

During development of the protocol we observed several categories of services, described below:

### Randomiser

A service which produces a random number or random outcome

Commonly used in gambling and other gaming applications, these need to be assessed based on the spread of values reported. A truly random service will, in aggregate, produce a spread of values across the set of outcomes targetted by the service.

### Model

A service which applies a model across a dataset

An example are Machine Learning Models, such as a Credit Scoring application used to assess an entity loan. The reliability / utility of these services are usually based on specific metrics such as Gini or Kolmogorov???Smirnov (KS) test.

### Price Oracles

A service which reports a currency or token exchange rate

On-chain reporting of exchange rates can be retrospectively compared against other exchanges to create metrics such as distance from mean for the same reporting period.

### Event Oracles

A service which verifies an event occurred

An authoritative peer reporting metric is required to confirm an event was recorded in a timely manner.

## Demonstrate reporting of metadata

A rudimentary interface which applies this protocol against the Cardano testnet can be found here: https://www.croesus-blockchain.com/

We have used a random-true and a random-fullum ("loaded dice") examples to demonstrate the utility of the concept.

## Lessons Learnt

* Meta data transactions written to the blockchain are permanent! Ensure that you get your protocol right on testnet before using mainnet!

* Meta data transactions are a great auto-discovery mechanism. A consistently applied protocol on the block-chain is a cheap, always-on network resource that can be queried with the right toolset.

* Simple building blocks like a consistently applied protocol can be scaled and subsequently used as components in other larger services.

## Unsolved Questions

* Does a reporting framework like this increase competition?

* Are the incentives to report (reputation, validations) more than the incentives to not report (public, permanent record of failures)

* What domains does this framework help, and which does it hurt?

* Can Oracle Pools use these metrics as part of governance?

## Future Work

* Perform a deep-dive into real-world use cases to validate the concept and potential business models of Oracles. Investigate with Fund 6 Proposal.

* Of particular interest to the team is the use of this protocol to support Reinforcement Learning for Machine Learning Models, as our approach can be extended to any type of automated service which needs a mechanism to demonstrate its reliability or utility.

Or thought experiments and proof of concepts can be mapped to three specific applications:

### Competiton

What if we had an ecosystem that had many nodes competing to provide the best credit risk algorithm? If all of the nodes periodically reported their results, a natural competitive market place would form.

### Reinforcement Learning

What if each node in the ecosystem could get better at predicting credit risk based on the raw data referenced in each of these reports? A natural reinforcement learning pattern would evolve.

### AI Service Selection

What if Artificial Intelligent agents could use this performance meta data to determine which node in the ecosystem is best to use depending on a particular purpose or context? A natural AI choice model would start to develop.

## [](#fund-7-proposal)Fund 7 Proposal - Cardano Risk Assessment Tool 

One area where the Croesus Protcol could best demonstrate its utility is via a Machine Learning Model service, such as a Cardano Risk Assessment Tool.

The model's output will be summarised as a Risk Score and provided via API as well as visually on a public web resource with data visualisations displaying the primary drivers of fraud risk.

For this initial development, the model will be trained on fraud data from already known, valuable resources in the Cardano community such as the [Cardano Phishing Bot](https://twitter.com/CardanoPhishing "Cardano Twitter Phishing Bot").

![Cardano Risk Assessment Tool Mockup](/F8E0F067-9837-4880-B5A4-68F506A0DF72.png)



