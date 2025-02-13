# AppSecAI-Public-Benchmarks
This repository is intended to house triage and remediation benchmarks made public by AppSecAI. 

## OWASP Benchmark
> The OWASP Benchmark Project is a Java test suite designed to verify the speed and accuracy of vulnerability detection tools. It is a fully runnable open source web application that can be analyzed by any type of Application Security Testing (AST) tool, including SAST, DAST (like ZAP), and IAST tools. The intent is that all the vulnerabilities deliberately included in and scored by the Benchmark are actually exploitable so its a fair test for any kind of application vulnerability detection tool. The Benchmark also includes scorecard generators for numerous open source and commercial AST tools, and the set of supported tools is growing all the time.
>
> The project documentation is all on the OWASP site at the OWASP Benchmark project pages. Please refer to that site for all the project details.
>
> The current latest release is v1.2. Note that all the releases that are available here: [https://github.com/OWASP/Benchmark/releases](https://github.com/OWASP/Benchmark/releases) are historical. The latest release is always available live by simply cloning or pulling the head of this repository (i.e., `git pull`).
- https://github.com/OWASP-Benchmark/BenchmarkJava

AppSecAI leverages the OWASP Benchmark to measure the effectivenes of its Expert Triage Automation (ETA) and Expert Fix Automation (EFA) products. We hope that by publishing the benchmark, our raw results against it, and an analysis of our results, it will encourage other vendors in this space to publish metrics against our and other benchmarks. This will allow customers to make the most informed decisions regarding which products are the best fit for their needs.
