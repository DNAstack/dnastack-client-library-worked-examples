# DNAstack Publisher/Explorer Workflow Examples


## One task Three Ways

This repo demonstrates a very simple task using the `dnastack` command line tool, using multiple different execution engines.

### Getting Started

```bash
git clone git@github.com:DNAstack/dnastack-client-library-worked-examples.git
cd dnastack-client-library-worked-examples
```

### Wdl

#### MiniWDL

[MiniWDL](https://github.com/chanzuckerberg/miniwdl) started as a set of python bindings for the WDL language. Since its early days, it has now become a fully fledged execution engine, capable of running workflows at scale through docker-swarm (and soon, `kubernetes`).

```bash
pip install miniwdl
miniwdl run examples/wdl/02_download_collection_files.wdl
```

#### Cromwell

[Cromwell](https://github.com/broadinstitute/cromwell) is the original execution engine for WDL and can be run in either server or command line mode. It supports running thousands of jobs concurrently and is highly configurable to support a large number of different execution engines.

```bash
wget https://github.com/broadinstitute/cromwell/releases/download/63/cromwell-63.jar
java -jar cromwell-63.jar run examples/wdl/02_download_collection_files.wdl
```

### Cwl

[CWL](https://www.commonwl.org/) is not a software, but a specification (similar to WDL) that describes a worklfow. It can be used to define individual tasks or to chain a series tasks together into a workflow.

```bash
sudo apt-get update
sudo apt-get install cwltool

./examples/cwl/02_download_collection_files.cwl
```

### Nextflow

[Nextflow](https://nextflow.io) is a relatively new vertical execution stack for bioinformatics (meaning it defines its own domain-specific language (DSL) and execution service). It takes a unique approach by providing a groovy-based DSL that is reactive streams-based.

```bash
wget -qO- https://get.nextflow.io | bash
nextflow run --config examples/nextflow/nextflow.config examples/nextflow/02_download_collection_files.nf
```

If you are using [Nextflow Tower](https://tower.nf) to monitor the pipeline, you can add a `scope` to your config like the following:

```bash
docker.enabled = true
tower {
    enabled = true
    accessToken = '<YOUR TOKEN>'
}
```
