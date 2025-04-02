# FBAD

This repository contains C++ codes and datasets for the paper:

> A Gradient Projecting-based Approach for Efficient Densest Subgraph Discovery on Large Directed Graphs

## Introduction

In this paper, we study the problem of the directed densest subgraph (DDS) problem on directed graph. Presenting both practically and
theoretically efficient DDS discovery algorithms by employing projecting FISTA and a few optimizing techniques, we have performed extensive experimental evaluation on 15 real-world large graphs and the results demonstrate the high efficiency of our algorithms.

## Environment

The codes of our in-depth study are implemented and tested under the following development environment:

- Hardware : Intel(R) Xeon(R) Gold 6338 CPU @ 2.00GHz and 512GB of memory.
- Operation System : Ubuntu 20.04.5 LTS (GNU/Linux 5.15.0-101-generic x86_64)

## Datasets

We use 15 real-world datasets from different domains, which are mainly downloaded from the [Stanford Network Analysis Platform](http://snap.stanford.edu/data/) and [Networks](http://konect.cc/networks/).



### Table: Datasets used in our experiments.

| Dataset | Category | \|V\| | \|E\| |
|---------|----------|-------|-------|
| Maayan-Lake (ML) | Foodweb | 183 | 2,494 |
| Moreno-Oz (MO) | Social | 217 | 2,672 |
| Traffic-Control (TC) | Infrastructure | 1,126 | 2,615 |
| Maayan-Figeys (MF) | Metabolic | 2,239 | 6,452 |
| OpenFlights (OF) | Infrastructure | 2,939 | 30,501 |
| Advogato (AD) | Social | 6,541 | 51,127 |
| Email-EU (EU) | Comments | 265,214 | 420,045 |
| Amazon (AM) | E-commerce | 403,394 | 3,387,388 |
| WikiTalk (WT) | Communication | 2,394,385 | 5,021,410 |
| Amazon-ratings (AR) | E-commerce | 3,376,962 | 5,838,041 |
| Baidu-Zhishi (BA) | Hyperlink | 2,141,300 | 17,794,839 |
| Wikipedia-Link (WL) | Hyperlink | 759,923 | 20,546,603 |
| EW-2013 (EW) | Social | 4,206,785 | 101,355,853 |
| Wiki-En (WE) | Hyperlink | 13,593,032 | 437,217,424 |
| SK-2005 (SK) | Web | 50,636,154 | 1,949,412,601 |


## How to Run the Codes


### A. Code Compilation


After cloning the codes from GitHub, use the following command to compile the codes in the repository :


```sh

cmake CMakeLists.txt

make ./DensestSubgraph

```


### B. Command Line Parameters

A general command of our program is like:

```sh

./DensestSubgraph [-option1 value1] [-option2 value2] ...

```

For example, you could run `core-exact` on DP in the following command:

```sh

./DensestSubgraph -path ./data/DP.txt -t u -a e -red core-exact -alloc flow-exact -ext flow-exact -ver flow-exact

```

There are a lot of options for you to conduct a thorough evalution among different algorithms:

|Parameters| Value            |Description|
|:---------------|:-----------------|:------------|
|-path| ---              |path to the dataset|
|-t| `u`, `d`         |`u`: undirected, `d`: directed|
|-a| `e`, `a`         |`e`: exact, `a`: approximation|
|-eps| $\epsilon\ge0$   |error threshold for $1+\epsilon$ approximation algorithms|
|-red| refer to B1      |method of *graph reduction*|
|-alloc| refer to B2      |method of `VWU`|
|-ext| refer to B3      |method of *candidate subgraph extraction*|
|-ver| refer to B4      |method of *candidate subgraph verification*|
|-seq| `t`, `f`         |`t`: sequential update strategy, `f`:  simultaneous update strategy|
|-vw| `t`, `f`         |`t`: transform DDS problem into vertex-weighted UDS problem, `f`: do not transform|
|-gamma| $0\le\gamma\le1$ |a parameter that controls the lower bound of binary search|
|-exp| `t`, `f`         |`t`: iteration number grows exponentially, `f`: iteration number is fixed|
|-it| integer, $it\ge1$|fixed iteration number|
|-dc| `t`, `f`         |`t`: apply divide-and-conquer strategy, `f`: do not apply|
|-ra| `t`, `f`         |ablation study on *graph reduction*, `t`: print reduction ratio, `f`: do not print|
|-res| `t`, `f`         |`t`: restrict $xy-core$ in a tight interval, `f`: do not restrict|
|-width| $width\ge1$      |a parameter that controls the tightness of interval|
|-multi| `t`, `f`         |`t`: apply multi-round reduction, `f`: apply single-round reduction|


#### B1. Methods of *Graph Reduction*

|Value|Description|
|--------|--------|
|`k-core`|derive a $k-core$, support UDS algorithms|
|`stable`|derive a stable set|
|`exact-xy-core`|derive an exact $xy-core$, support DDS algorithms|
|`appro-xy-core`|derive an approximate $xy-core$, support DDS algorithms|
|`w-core`|derive an $w^*-core$, support WCoreApp algorithm|


#### B2. Methods of `VWU`

|Value|Description|
|--------|--------|
|`flow-exact`|the `VWU` method of `FlowExact`, `CoreExact`, `DFlowExact`, `DCExact`|
|`fw`|the `VWU` method of `FWExact`, `FWApp`, `DFWExact` and `DFWApp`|
|`fista`|the `VWU` method of `FISTAExact` and `FISTAApp`|
|`mwu`|the `VWU` method of `MWUExact` and `MWUApp`|
|`core-app`|the `VWU` method of `CoreApp`|
|`greedy`|the `VWU` method of `Greedy` and `DGreedy`|
|`greedypp`|the `VWU` method of `Greedy++`|
|`flow-app`|the `VWU` method of `FlowApp`|
|`xy-core-appro`|the `VWU` method of `XYCoreApp`|
|`w-core-appro`|the `VWU` method of `WCoreApp`|


#### B3. Methods of *Candidate Subgraph Extraction* (`CSE`)

|Value|Description|
|--------|--------|
|`flow-exact`|the `CSE` method of `FlowExact`, `CoreExact`, `DFlowExact`, `DCExact`|
|`cp`|the `CSE` method of `FWExact`, `FWApp`,`FISTAExact` ,`FISTAApp`, `MWUExact`, `MWUApp`, `DFWExact` and `DFWApp`|
|`core-app`|the `CSE` method of `XYCoreApp` and `WCoreApp`|
|`greedy`|the `CSE` method of `DGreedy`|


#### B4. Methods of *Candidate Subgraph Verification* (`CSV`)

|Value|Description|
|-------------|--------|
|`flow-exact`|the `CSV` method of `FlowExact`, `CoreExact`, `DFlowExact`, `DCExact`|
|`cp`|the `CSV` method of `FWExact`, `FWApp`,`FISTAExact` ,`FISTAApp`, `MWUExact`, `MWUApp`, `DFWExact` and `DFWApp`|
|`core-app`|the `CSV` method of `CoreApp`|
|`flow-app`|the `CSV` method of `FlowApp`|
|`greedy`|the `CSV` method of `DGreedy`|



### C. Data Download


You can download the datasets from the following Google driven link:


XXXXXXXXXXXXXXXXXX


### D. Experimentation


Our one-click script for reproducibility is comming soon.


[//]: # (### E. Contact)

[//]: # ()
[//]: # ()
[//]: # (If you have any questions about the code or find any errors, please list them in the `issue` or contact us directly by email:)

[//]: # ()
[//]: # ()
[//]: # (`yiyang3@link.cuhk.edu.cn` , `qingshuoguo@link.cuhk.edu.cn` or `yinglizhou@link.cuhk.edu.cn`)
