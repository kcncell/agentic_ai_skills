---
name: literature-search
description: Orchestrates scientific literature searches, summaries, and downloads across multiple sources. Trigger when the user uses the /literature-search slash command.
---

# Literature Search Orchestration

You are responsible for executing the `/literature-search` command workflow. This command has three sub-actions: `search`, `summarize`, and `download`.

## 1. `/literature-search search <source> <keywords>`
When the user issues this command:
1. **Search Tool**: Map the `<source>` to the appropriate existing tool/database (e.g., `pubmed-database` for pubmed, `literature-search-arxiv` for arXiv, `literature-search-biorxiv` for bioRxiv, or `literature-search-europepmc`/`literature-search-openalex` for general journals like Nature/Science).
2. **Execute Search**: Find the top 10 relevant papers for the given `<keywords>`.
3. **Summarize (Level 1)**: For each of the 10 papers, generate a 500-1000 word summary containing:
   - Objective
   - Brief Method
   - Discussion & Conclusion
4. **Save**: Save this compilation as a text file named exactly `[YYYY-MM-DD]_[source].txt` (e.g., `2026-07-09_pubmed.txt`) inside `/Users/username/Documents/1_Work/2_Research/Journals/daily_summary_feed/`.
5. **Report**: Output a brief confirmation to the user and list the 10 papers (with index 1-10) so they can choose which ones to dive deeper into.

## 2. `/literature-search summarize <indices>`
When the user issues this command (e.g. `/literature-search summarize 3, 5, 9`):
1. **Recall**: Look up the papers corresponding to the requested indices from the most recent `/literature-search search` output.
2. **Deep Summarize (Level 2)**: For each requested paper, generate a highly detailed 10,000 - 15,000 character summary in plain English. Avoid heavy technical jargon where possible, aiming to make it simple and easy to understand (about 1/4th of the original paper's length).
3. **Save**: Save each summary as a `.txt` file in the appropriate topic subfolder under `/Users/username/Documents/1_Work/2_Research/Journals/`. The filename MUST follow the standard convention: `[Year Published]_[Last Name]_[First Name (1st Author Only)]_[First Few Words of Title].txt` (with NO spaces in the filename).

## 3. `/literature-search download <indices>`
When the user issues this command:
1. **Recall**: Look up the papers corresponding to the requested indices from the most recent search.
2. **Download**: Download the full-text PDF for each paper. Write scripts or use existing tools to fetch the PDF safely.
3. **Save & Rename**: Save the PDFs in the appropriate topic subfolder under `/Users/username/Documents/1_Work/2_Research/Journals/`. The filename MUST follow the exact standard convention: `[Year Published]_[Last Name]_[First Name (1st Author Only)]_[First Few Words of Title].pdf` (with NO spaces in the filename).

## General Rules
- **Naming Convention**: You must stringently adhere to the file naming convention `[Year Published]_[Last Name]_[First Name (1st Author Only)]_[First Few Words of Title].[ext]` with no spaces for individual paper downloads and deep summaries.
- **Topic Folders**: Do not invent new topic folders; categorize papers into existing subfolders under `/Users/username/Documents/1_Work/2_Research/Journals/` whenever possible.
- **Aggregation**: If a source like "Nature" or "Science" is requested, use OpenAlex or EuropePMC to search those specific journals.
