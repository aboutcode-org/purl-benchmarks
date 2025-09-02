# AboutCode PURL Accuracy Benchmark Guide

## Problem

Public studies of SBOMs have demonstrated that the biggest hurdle to SBOM
effectiveness, when shared among producers and consumers, is the quality of the
software identifiers, especially the need for those identifiers to be precise
and machine-processable. The PURL standard supports precise, accurate, high-
quality software identification.

## Objective

Provide guidance to improving the accuracy of PURLs (Package URLs) constructed
by SCA tools by making use of a shared, open, public, and agreed-upon baseline
of the list of PURLs that must be found when scanning a given test input
codebase.

## Resources

AboutCode PURL benchmarks are reference lists of expected PURLs, for a variety
of public projects that can be used to demonstrate and validate the detection of
correct PURL values. Planned tested input projects include PURL lists derived
from:

* A base RedHat container image (UBI)  
* A base Debian or Ubuntu container image  
* A large Go-based web application (with k8s)  
* A large Python-based web application  
* A large Java/JS-based application

The AboutCode PURL benchmark files are in a simple .txt format. They are a
sorted list of expected PURL values to be found when analyzing an input
codebase.

The AboutCode PURL benchmark files were originally generated using standard
[ScanCode.io](http://ScanCode.io) pipelines, and other open source tools, and
were carefully reviewed for correctness by expert analysts. They form a
community digital commons asset and we expect careful scrutiny and community
contributions to ensure these represent the ground source of truth that should
be reported by any tool.

See table in the section "PURL Benchmark Tested Inputs and Expected Outputs" for
detailed PURL benchmark data.

## PURL Benchmark Accuracy Procedure

* Download (1) a software project that provided the input basis for a PURL
  benchmark. We call this the tested input codebase.

* Download (2) the corresponding benchmark file with a list of expected PURLs
  that have been curated for this tested input
* Use your selected SCA tool to analyze the downloaded software codebase.  
  * If possible, configure your SCA tool to generate an output file that is a simple text list of PURL values; or,
  * Generate an SBOM with your SCA tool; and,  
    * Either extract a simple list of PURL values for a manual comparison with the expected PURLs; or
    * Use the SBOM in SPDX or CycloneDX JSON format for use with the "benchmark\_purls" ScanCode.io pipeline
* Compare your generated output with the PURL benchmark. This comparison can be done:  
  * Manually reviewing the two sorted lists of PURLs,  
  * Using a diff utility,  
  * Using the "benchmark\_purls" ScanCode.io pipeline that takes as input a tested SBOM and an expected PURLs list.

* When reviewing the comparison results, pay special attention to:   
  * The percentage of exact PURL matches between the tested and expected PURL 
  * Mis-matches on each of the PURL components for partially matched PURLs
    (https://github.com/package-url/purl-spec/blob/main/purl-specification.md).
  * Missing PURLs: PURLs that are in the benchmark but not in your output.  
  * Extraneous PURLs: PURLs that are in your output but not in the benchmark.  
  * Consider these matching patterns for each of your PURL components:  
* **scheme**: should always have a constant value of "pkg". Required.  
* **type**: the package "type" or package "protocol" such as maven, npm, nuget,
  gem, pypi, etc. Required.  
* **namespace**: some name prefix such as a Maven groupid, a Docker image owner,
  a GitHub user or organization. Optional and type-specific.  
* **name**: the name of the package. Required.  
* **version**: the version of the package. Optional, but strongly recommended.  
* **qualifiers**: extra qualifying data for a package such as an OS,
  architecture, a distro, etc. Optional and type-specific.  
* **subpath**: extra subpath within a package, relative to the package root. Optional.  
* Take action on each mis-match to improve your tool capabilities:  
  * Visit the purl-spec to get detailed guidance about the problem area
    https://github.com/package-url/purl-spec/blob/main/purl-specification.md , or  
  * If you think the AboutCode PURL benchmark value is wrong, or could be
    improved, please log an issue describing exactly what you found so we can
    amend the expected PURLs results for a tested input.

## PURL Benchmark Tested Inputs and Expected Outputs

This table contains the download URLs  for tested input codebass and the
corresponding filename of the expected PURLs list.

The expected PURLs files are stored in the `expected-PURLs` directory.

| Input name | Input version | Download URL | Expected PURLs filename | Notes |
| :---- | :---- | :---- | :---- | :---- |
| alpine | 3.22.1 | docker://alpine:3.22.1 | alpine-3.22.1-purls.txt | An Alpine container image |
| debian | trixie | docker://debian:trixie | debian-trixie-purls.txt | A Debian container image |
| django | 5.2.5 | https://files.pythonhosted.org/packages/py3/d/django/django-5.2.5-py3-none-any.whl | django-5.2.5-whl-purls.txt | A Python package|
| fiber | 2.52.9 | https://github.com/gofiber/fiber/archive/refs/tags/v2.52.9.tar.gz | fiber-2.52.9-purls.txt | A go package |
| gin | 1.10.1 | https://github.com/gin-gonic/gin/archive/refs/tags/v1.10.1.tar.gz | gin-1.10.1-purls.txtt | Another go package |
| sentry | 25.7.0 | https://github.com/getsentry/sentry/archive/refs/tags/25.7.0.tar.gz | sentry-25.7.0-purls.txt | A Python and Rust application |
| ubuntu | 24.04 | docker://ubuntu:noble | ubuntu-24.04-purls.txt | A Ubuntu container image |



## PURL Benchmark Automation in ScanCode.io

Using the expected PURLs file list and an SBOM, follow these instructions to run a benchmark:

https://scancodeio.readthedocs.io/en/latest/built-in-pipelines.html#benchmark-purls-addon


To run a benchmark you can use:

1. The expected PURLs files stored in the `expected-PURLs` directory.
2. Corresponding pre-computed sample CycloneDX SBOMs from the `sample-SBOMs` directory.


