# Semiconductor Manufacturing Quality Analysis

Applying **Statistical Process Control (SPC)** and **Lean Six Sigma** tools to real production data from a semiconductor fabrication line, to find which process parameters drive product failures and whether the process is stable and capable.

[

![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)

](https://colab.research.google.com/github/fai-algethami/secom-quality-analysis/blob/main/SECOM_Quality_Analysis.ipynb)

## Business question
A fab runs hundreds of in-line sensors, but engineers cannot watch all of them. **Which few parameters matter most for yield, and are they under control?**

## Data
[UCI SECOM dataset](https://archive.ics.uci.edu/dataset/179/secom): 1,567 production runs, 590 sensor measurements per run, each labelled Pass/Fail at final test (Jul–Oct 2008). The notebook downloads it automatically.

## Approach
| Step | Method | Quality tool |
|---|---|---|
| 1. Data quality | Remove sensors that are mostly empty or constant | Measurement system check |
| 2. Yield | Overall and weekly failure rate | Run chart |
| 3. Root-cause screening | Rank sensors by gap between failed and passed runs | **Pareto analysis** |
| 4. Stability | Control limits from moving range (MR̄/1.128) | **I-MR control charts** |
| 5. Capability | Compare first vs second half of production | **Cpk** |
| 6. Action | Findings + recommendations | DMAIC mindset |

## Key results
- **Line yield: 93.4%** (104 failed runs out of 1,567).
- **Data quality gap:** 144 of 590 sensors (24%) were unusable, mostly empty or constant, pointing to a data-collection problem in the fab.
- **Key sensors linked to failures:** S59, S103, S510.
- **Out-of-control runs fail 2–3× more often:**

| Sensor | Out-of-control runs | Failure rate (out of control) | Failure rate (in control) |
|---|---|---|---|
| S59 | 129 | 13.2% | 6.1% |
| S103 | 56 | 14.3% | 6.4% |
| S510 | 57 | **19.3%** | 6.2% |

- **Process capability (Cpk), first vs second half of production:**

| Sensor | Cpk first half | Cpk second half | Trend |
|---|---|---|---|
| S59 | 0.65 | 1.69 | Improved |
| S103 | 0.70 | 0.54 | Worsened |
| S510 | 0.37 | 0.44 | Not capable in either half |

**Recommendations:** put S59, S103 and S510 on real-time SPC monitoring with alarms; investigate root causes of out-of-control runs (equipment, recipe, material lot), starting with S510; repair data collection for sensors with mostly missing readings.

## Assumptions & limitations
- SECOM does not publish specification limits, so Cpk uses **assumed limits** from passing runs in the first half of production.
- Sensor names are anonymised in the source data, so findings point to *which* signals to investigate, not the physical cause.
- This is association, not proven causation; confirming root cause would need process engineering input (DMAIC Analyze/Improve).

## How to run
1. Click **Open in Colab** above (no installation needed).
2. `Runtime → Run all`.

## Tools
Python · pandas · matplotlib · SPC · Pareto · Cpk · Lean Six Sigma

## Author
**Fai Algethami** · Applied Physics · Saudi Semiconductor Program (SSP), Advanced Semiconductor Fabrication Track

*Data: McCann, M. & Johnston, A. (2008). SECOM. UCI Machine Learning Repository.*
