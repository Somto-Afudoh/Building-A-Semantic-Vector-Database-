## Prompt log

### 2026-10-09

> Say you are a senior data engineer reviewing the repo, walk me through how the pipeline works, it's tasks, the sources, destinations and any lines of code that is costly (both technically and potentially when deployed to production).  
> guide me through the data quality plan for the pipeline. use the following files as reference #transformation.py #ingestion.py #load_gold.py
>
> Note the following:
> - kindly log this prompt in the #COPILOT_LOG.md and fill every prompt i will send to you here.
> - when reviewing the code, point to the file and line that has the problem and explain why it is a problem from a technical and layman pov, and suggest solutions to the problem. do not rewrite the code. Say so if you are unsure.
>
> map/ explain how the pipeline works, every problems found, solutions suggested will be written as part of the document in the #README.md
>
> Now lets Go

### 2026-10-10

> is the suggested solution you gave for 'ingestion.py:21-23' which"Define a deterministic “current/best” metadata rule and measure duplicate/conflict rates before deduplicating." better than  "spark to explicitly keep the first row according to an ordering rule" and why so

**Answer summary:** These recommendations complement one another: define the business meaning of “best” (for example, newest valid source record), then implement it with a deterministic ordering and tie-breaker. Measuring duplicate/conflict rates informs and validates that policy but does not choose the winner.

**Evidence check:** Confirmed against `ingestion.py:17–22`: `drop_duplicates(["metadata_parent_asin"])` selects a row without an ordering or precedence rule. No such current/best policy is encoded in the script.

### 2026-10-10 — milestone review requests

> Say you are a senior data engineer reviewing the rep
>
> 1. ### Map the pipeline
> Use Copilot to explain each script, check it against the code, and draw the architecture.
>
> 1. ### Audit the code
> Work through the checklist. Give every finding evidence, a severity, and its impact on AeroMart.
>
> 1. ### Propose improvements
> Rewrite the code for your top five problems and explain every changed line.
>
> 1. ### Plan for data quality
> Design at least eight checks for Silver and Gold, drafted with Copilot and reviewed by you.
>
> 1. ### Document everything
> README, data dictionary, docstrings, and a log of where Copilot helped and where it misled you.
>
> compared the commented out code on transformation to the udf used

**Answer summary:** This broad request was followed by a narrower request focused on checking Milestone 1. No code rewrite, complete audit, or eight-check data-quality deliverable was undertaken in response to the broad request.

**Chunker comparison:** The commented implementation targets about 400 characters with 50-character overlap and separator-aware boundaries; the active UDF uses windows of up to 60 words with 10-word overlap, without sentence-aware boundaries. Neither function recursively calls itself. Both catch all exceptions and return an empty list. Confirmed by comparing `transformation.py:20–43` with `transformation.py:45–72`.

**Assessment:** Scope noted; the later request directs this review to Milestone 1 and asks that later unfinished milestones be identified.

> Say you are a senior data engineer reviewing the repository. Following the outlined milestones I would love you to check the first milestone at #CASE_STUDY.md which is Map the pipeline and draw the architecture against the repo and know if there are any missing milestones undone
>
> 1. ### Map the pipeline
> Use Copilot to explain each script, check it against the code, and draw the architecture.
>
> Note:
>
> Create a file names ARCHITECTURE.md and save the architecture drawing of the maped pipeline.
>
> Use the information provided in #CASE_STUDY.md to complete this task

**Answer summary:** Created `ARCHITECTURE.md` with a Mermaid architecture diagram, stage inputs/outputs, code-derived column lineage, operational limitations, and milestone status. Added the detailed column map to README and recorded this prompt and the preceding broad request.

**Evidence check:** Confirmed against `ingestion.py:14–45`, `transformation.py:13–18,45–72,74–101`, and `load_gold.py:15–32`, plus `CASE_STUDY.md` milestone requirements. The paths and columns are code-derived; source input data was not present and the pipeline was not run. Milestone 1's deliverables are marked complete; milestones 2–5 remain incomplete as described in `ARCHITECTURE.md`.

### 2026-10-11

> let us complete the second milestone on Audit the code. Create a file called AUDIT_REPORT.md and write the following Audit report in it.!
>
> Work through the checklist on #CASE_STUDY.md. For every checklist ID, give me a status (Confirmed or Not an issue), the file and line numbers, a severity (High, Medium, or Low), and the impact on AeroMart. Add any problems you found that are not on the list.
>
> Note:
> **Done when:** every ID has a status and evidence, and the report opens with the top five problems in priority order.
> The findings are saved in the audit report file created

**Answer summary:** Created `AUDIT_REPORT.md` with the five prioritized risks first, then all 46 checklist IDs (A-1 through F-4), each with status, file/line evidence, severity, and AeroMart impact, plus three additional findings. Updated README and architecture milestone status.

**Evidence check:** Checklist items were checked against source scripts, `demo.ipynb`, requirements, `.gitignore`, README, and repository file listing. This is a static audit; the pipeline was not run and Bronze input files are unavailable. Runtime-dependent behavior, actual data prevalence, model cache/network state, and quantified production cost are stated as unverified where applicable.

Future prompts in this conversation should be appended here as additional dated entries when received.