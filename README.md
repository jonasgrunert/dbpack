# DBPack

This is a CLI to make developing for the Oracle MLE Databse Plugin easier.

here is abit of explanation, on how to get going:
## Instructions

There are multiple steps necessary to perform the benchmark. We are showing detailed steps to execute them on a Linux Distribution in our case Ubuntu. The deployment process can be divided into three phases:

1. Setup Environment and install all tools
2. Launch and prepare database
3. Execute benchmark

#### Phase 1: Install dependencies

1. Install [Docker](https://docs.docker.com/install/linux/docker-ce/ubuntu/) and [Docker-Compose](https://docs.docker.com/compose/install/) on your machine.

2. Download the [MLE Docker Image](https://www.oracle.com/technetwork/database/multilingual-engine/downloads/index.html) and add the image to docker by executing `docker load --input mle-docker-0.3.0.tar.gz`

3. Install [sqlloader and sqlplus](https://docs.oracle.com/cd/B19306_01/server.102/b14357/ape.htm) and add both programs to your PATH.

4. Install at least [NodeJS 10.6](https://nodejs.org/en/download/current/) and at least [Python 3.6](https://www.python.org/downloads/).

5. Download [our code](https://github.com/hpi-swa-lab/pp19-4-stored-procedures) which is currently distributed via git. You can clone it using https://github.com/hpi-swa-lab/pp19-4-stored-procedures.git.

6. Install all dependencies for the benchmarks. To install all dependencies for ATP and ELO go to the root folder of each algorithm and use [npm](https://www.npmjs.com/get-npm) with the command `npm install`.

7. Install all dependencies for the deployment tool tsdb by executing `npm install` in the tsdb folder. Then compile it by using `npm run compile`.

8. Install typescript globally using `npm i -g typescript`.

### Phase 2: Using dbpack

It offers a wide variety of options, which will be briefly covered here.

To use the dbpack deployment script execute `dbpack pack <file>`. At the moment there is only one command `pack`. All other information you can receive using `--help`. The options are listed below:

dbpack pack [file]

packing the function a single time

Positionals:
file Name of you entry point file [string]

Options:

| shorthand | option       | description                              | type    | default     |
| --------- | ------------ | ---------------------------------------- | ------- | ----------- |
|           | --help       | Show help                                | boolean |             |
|           | --version    | Show version number                      | boolean |             |
| -t        | --tsConfig   | Path to TSConfiguration file             | string  | false       |
| -r        | --ruConfig   | Path to RollUpConfiguration file         | string  | false       |
| -v        | --verbose    | This makes tsdb talk a lot               | boolean | false       |
| -e        | --emitFiles  | This option controls the output of files | boolean | false       |
| -n        | --name       | This sets a custom name for the module   | string  | "dbmodule"  |
| -c        | --connection | Connection string of the database        | string  | ""          |
| -s        | --emitStats  | Let stats be emitted from rollup         | boolean | false       |
|           | --tablename  | Table name where to put the src modules  | string  | "dbmodules" |
| -p        | --dbpassword | Password to access database              | string  | "system"    |
| -u        | --dbuser     | Username to access database              | string  | "password"  |


For everyone who is interesed in a more differentiated and explorative view of the topic here you go with an introduction: (The entire repo,  is at the moment unavailabe.)

## Abstract

In this years project seminar Polyglot Programming, we investigated the use of modern programming languages like JavaScript as stored procedures or stored functions by using Oracle's experimental feature for the Oracle Database 12c called Multi Lingual Engine (MLE). MLE uses GraalVM to execute scripts written in JavaScript and Python within the Oracle Database 12c.

If using a lot of stored data executing scripts directly on the database suggests a higher performance in comparison to a classical client-server approach due to the locality to the data. To examine the suggestion, we conducted a benchmark with two different algorithms written in TypeScript and transpiled to JavaScript.

ELO is a widely used algorithm to calculate the relative skill level of players for competitive games like chess. ELO uses stored data for each calculation. Available to promise (ATP) is an economical algorithm to determine if a specific product is available to a given time. ATP fetches data only once and calculates the result afterwards.

Based on the results of the benchmark, we can verify that algorithms which require a high data throughput like ELO execute faster if using MLE than executing the same algorithm in a node process, whereby algorithms which do not need a high data throughput like ATP are slower using MLE.
