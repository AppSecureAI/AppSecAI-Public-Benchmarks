# AppSecAI-Public-Benchmarks

This repository houses the publicly available triage and remediation benchmarks published by AppSecAI.

## OWASP Benchmark

> The [OWASP Benchmark Project](https://github.com/OWASP-Benchmark/BenchmarkJava) is a Java test suite designed to measure the speed and accuracy of vulnerability detection tools. It’s a fully runnable open source web application that can be analyzed by any type of Application Security Testing (AST) tool (e.g., SAST, DAST like ZAP, and IAST tools). The Benchmark deliberately includes exploitable vulnerabilities so that every type of AST tool has a fair chance to detect them. It also provides scorecard generators for several open source and commercial AST tools, and the list of supported tools continues to grow.
>
> All project documentation can be found on the [OWASP Benchmark project pages](https://owasp.org/www-project-benchmark/). Please refer to those pages for complete details.
>
> The most recent official release is **v1.2**. Note that all releases listed at [GitHub Releases](https://github.com/OWASP/Benchmark/releases) are historical. The latest version is always available by cloning or pulling the head of the repository (i.e., `git pull`).

AppSecAI uses the OWASP Benchmark to gauge the effectiveness of its **Expert Triage Automation (ETA)** and **Expert Fix Automation (EFA)** products. By making the benchmark, our raw results, and our analysis public, we hope to inspire other vendors to share their metrics against our benchmarks and others. Ultimately, this helps customers make more informed decisions about the tools that best fit their needs.

## How We Test

We measure our products against a range of open source and proprietary benchmarks. Over time, we plan to publish many of these benchmarks. One such benchmark is the **OWASP Benchmark**.

### Input for Triage Tests

We begin by scanning the **OWASP Benchmark v1.2** with a variety of open source and commercial SAST tools. Each tool generates an output file, which we then normalize and convert to [SARIF](https://docs.oasis-open.org/sarif/sarif/v2.1.0/sarif-v2.1.0.html) format. Our ETA platform takes this SARIF file as input, along with the path to the OWASP Benchmark source (which has already been cloned to our server).

### The Triage Process

Our ETA product processes each finding in the SARIF file—anywhere from 900 to 16,000 findings, depending on the SAST tool—and stores the results in our product database. The triage process involves analyzing the data related to each finding, mapping it to the corresponding source code, and then (using several approaches, including prompting an LLM) classifying the finding as either “vulnerable” or “not vulnerable.”

### Measuring Effectiveness

The OWASP Benchmark includes an [“expected results” file](https://github.com/OWASP-Benchmark/BenchmarkJava/blob/master/expectedresults-1.2.csv) that indicates whether each test case is vulnerable. We use this file, along with manual labeling of any SAST findings not referenced in the expected results, to build a comprehensive “ground truth” that we compare against our product’s output.

#### Key Metrics

We track several key metrics to understand our performance against any dataset—and within specific portions of each dataset (such as particular vulnerability classes or languages). Below are the metrics we collect for each run of our ETA product:

- **True Positives (TP):** Actual vulnerabilities (confirmed by the Benchmark or by manual review) that the SAST tool correctly reports.
- **False Positives (FP):** Non-vulnerabilities (Benchmark “traps” or incorrectly flagged code) that the SAST tool mistakenly reports as vulnerabilities.
- **True Negatives (TN):** Non-vulnerabilities that the SAST tool correctly does not flag.
- **False Negatives (FN):** Actual vulnerabilities that the SAST tool fails to report.

##### Composite Metrics

While raw counts of true and false positives are useful, composite metrics offer a broader view of our performance:

- **True Positive Rate (TPR) = TP / (TP + FN)**  
  Measures how often the tool identifies real vulnerabilities correctly.
- **False Positive Rate (FPR) = FP / (FP + TN)**  
  Measures how often the tool incorrectly flags non-vulnerable code as vulnerable.
- **Benchmark Score (Youden Index) = TPR – FPR**  
  Gauges the tool’s balance between finding real vulnerabilities and avoiding false alarms.
- **Accuracy = (TP + TN) / (TP + FP + TN + FN)**  
  The proportion of correct classifications out of all possible classifications.
- **F1 Score = (2 × TP) / (2 × TP + FP + FN)**  
  A balanced measure of precision and recall, reflecting overall performance.
