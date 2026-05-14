# Shovel-Ready Trap Research Pipeline Design

Date: 2026-05-13

## Context

The repo already has the right outer shell for the requested work: `meta/` can orchestrate papers, `pipeline/` can run reviewer-style checks and build RAG/release artefacts, `papers/` holds source ledgers and manuscripts, `papers-out/` stores generated public snapshots, `docs/` is the website, and `plugins/` exposes the workflow locally.

The new paper should use that machinery rather than become a one-off manuscript. The user wants an imaginative regional-science contribution, not a criticism of the field and not another card-flow/local-spending paper. The strongest direction from the live OpenAlex scan is a paper on the project-conversion middle of regional development: places do not only differ in need, endowments, institutions, or outcomes; they also differ in their capacity to turn policy opportunities into bids, awards, procurements, contracts, and delivered interventions.

Working title: **The Shovel-Ready Trap: Project Pipelines and the Uneven Capacity to Do Regional Development**.

## Research Contribution

The paper adds a new empirical object to regional science: the **project pipeline**. Its central claim is that regional inequality can be reproduced inside the implementation funnel:

```text
need -> imagined project -> bid -> award -> procurement -> contract -> delivery
```

The contribution is not that place-based policy is bad, nor that regional science has missed institutions. The contribution is sharper: much of the literature studies need, allocation, treatment, resilience, development traps, institutional thickness, innovation systems, and outcomes after intervention. This paper measures the conversion process between policy opportunity and delivered project.

The paper will argue that competitive and projectified regional policy creates a "shovel-ready trap": places with greater governance bandwidth, fiscal slack, consultant access, planning capacity, and pre-existing project shelves are more able to convert funding windows into executable projects, while high-need places may be filtered out before impact evaluation ever begins.

## Literature Strategy

Use OpenAlex as the corpus backbone for the last five years of open-access regional science. The pipeline should collect metadata for works from 2021-05-13 through 2026-05-13 using a broad regional-science topic set plus core journals. It should store metadata, abstracts, OA links, and full-text URLs where OpenAlex exposes them.

The corpus is used for three purposes:

- Map the recent literature around left-behind places, regional development traps, resilience, place-based policy, institutions, planning, public investment, procurement, and green/industrial transitions.
- Build a cited reference base for the manuscript and evidence ledger.
- Support the website/RAG layer with summaries and retrieval records that reviewers can inspect.

The corpus pull must be reproducible and bounded. It should cache raw OpenAlex pages, normalize works into JSONL, and record query filters and timestamps. Full text should be downloaded only for open-access URLs that are available without login, with polite retry/backoff and provenance records. PDF text extraction is optional for v1; abstracts and available plain-text locations are enough for the first paper draft, but the architecture should leave a slot for later full-text extraction.

## Empirical Strategy

The best initial empirical domain is the UK because it has visible competitive funding rounds, open procurement data, local authority geographies, and strong policy relevance for regional science.

Primary data candidates:

- Levelling Up Fund bids, winners, rejected bids, round timing, project descriptions, values, and geographies.
- Towns Fund, Future High Streets Fund, Community Renewal Fund, and UK Shared Prosperity Fund allocations.
- Contracts Finder and Find a Tender notices for regeneration, transport, high streets, skills, housing, net zero, and infrastructure projects.
- Local planning/application data where available through planning.data.gov.uk or local authority open registers.
- Local authority reserves, spending power, staff/capacity proxies, and fiscal stress indicators.
- ONS measures for deprivation, productivity, employment, claimant count, population, rural-urban class, and local economic structure.
- Governance and political controls where available, including authority type and mayoral/combined authority membership.

The first empirical deliverable should be a project-conversion panel or event dataset by local authority and funding window. The minimum viable version should estimate:

- Which places bid less conditional on need.
- Which places win less conditional on bidding.
- Which places procure more slowly conditional on winning.
- Which places convert fewer awards into visible contracts.
- Whether capacity proxies explain conversion gaps after conditioning on need.

The paper should be explicit about uncertainty. The first version may use procurement notices as an imperfect delivery proxy. The ledger should mark that limitation and propose later validation against project completion reports, local authority accounts, or scheme-level monitoring data.

## Repository Design

Add a new paper under `papers/shovel-ready-trap/` with the same broad shape as `papers/scriptorship/`:

- `article/main.tex` and section files for the full paper.
- `article/references.bib` generated/curated from OpenAlex and policy sources.
- `evidence/claims.yml`, `evidence/sources.yml`, and `evidence/uncertainty_register.md`.
- `appendix/` for generated reviewer/RAG artefacts.
- `workflow/logs/` for run traces, corpus query logs, AI-use notes, reviewer passes, and decision logs.
- `workflow/prompts/` for literature sweep, synthesis, reviewer, revision, and data-building prompts.
- `data/openalex/` for cached metadata and normalized corpus records.
- `data/project_pipeline/` for source manifests and derived table schemas.

Register the paper in `meta/papers.yml` so `scriptor_meta.py publish-local --paper shovel-ready-trap` writes to `papers-out/papers/shovel-ready-trap/`, updates the website, builds an SSRN package, and records Overleaf status.

The first-page date footnote requirement remains: the new LaTeX paper must show a date note on page one, using the same convention as the existing paper.

## Pipeline Design

Add paper-specific scripts under `papers/shovel-ready-trap/scripts/` instead of overloading the reusable `pipeline/`:

- `openalex_fetch.py`: fetches and caches OpenAlex result pages for configured regional-science queries.
- `openalex_normalize.py`: converts raw pages into normalized JSONL with IDs, titles, years, venues, authors, abstracts, concepts/topics, OA status, URLs, DOI, cited-by count, and source query tags.
- `literature_map.py`: produces literature clusters, top works, gap notes, and candidate reference records for the evidence ledger.
- `project_data_manifest.py`: records intended UK project-pipeline data sources, URLs, access notes, fields, and refresh status.
- `draft_paper.py`: assembles a deterministic Markdown drafting packet from the literature map, evidence ledger, and empirical design notes. It should not pretend to have estimated results until derived data exists.

The reusable `pipeline/scripts/run_all_checks.sh` should remain the reviewer automation. The new paper must feed it valid claims and sources so it can build:

- claim dossiers;
- source dossiers;
- reviewer question bank;
- interrogation index;
- RAG query pack;
- adversarial audit report;
- overclaiming report;
- meta-transparency report;
- release summary;
- run manifest.

## Manuscript Design

The full-paper draft should be publishable as a serious working-paper scaffold, with clearly labelled estimate slots only where empirical estimates require downloaded/cleaned administrative data. It should include:

- title, abstract, keywords, and first-page date footnote;
- introduction motivating the project-conversion gap;
- literature review from OpenAlex-backed regional science sources;
- concept section defining project pipelines and the shovel-ready trap;
- data section specifying the UK sources and unit of observation;
- empirical strategy;
- expected mechanisms and testable hypotheses;
- preliminary descriptive agenda, clearly labelled until data are built;
- discussion of implications for regional development policy design;
- limitations and audit trail;
- conclusion;
- references.

Claims must be ledgered. Any strong claim about the literature, data, or expected mechanisms needs a claim ID, source links, warrant level, and uncertainty note where needed.

## Website And Outputs

The generated website should add a `shovel-ready-trap` page alongside `scriptorship`. It should expose:

- latest manuscript artefacts from `papers-out`;
- abstract and citation;
- SSRN package status;
- Overleaf status;
- RAG/summary page for the OpenAlex corpus and reviewer artefacts;
- generated claim/source dossiers and reviewer question bank.

The public output root remains configurable through `meta/papers.yml` and defaults to `papers-out/`. This keeps the GitHub-hosted version as the canonical folder rather than Dropbox.

## Overleaf And SSRN

Overleaf should be treated as a check-in target rather than the source of truth. The source of truth is the GitHub repo. For v1, Overleaf status may be a metadata/check file if an actual Overleaf git remote is not configured yet. Once a remote exists, the same adapter can push the article folder.

SSRN should be prepared as a package, not automatically submitted. The generated package should include title, abstract, an authors field, keywords, citation, manuscript source/PDF if available, and a release summary. This avoids pretending SSRN login/upload has happened while still making the submission bundle ready.

## Reviewer Passes

Reviewer automation should run in three layers:

1. **Mechanical release gate:** existing `run_all_checks.sh` validates claims, sources, warrant graph, overclaiming, dossiers, RAG pack, adversarial audit, run manifest, and release summary.
2. **Domain reviewer pass:** a generated reviewer memo asks whether the literature gap is real, whether the data strategy can identify pipeline conversion, whether mechanisms are confounded by need/quality/politics, and whether policy implications overreach.
3. **Revision pass:** the paper is revised against the reviewer memo, and the decision log records accepted and rejected changes.

The initial proof of concept should run the mechanical pass and generate the domain reviewer memo. It does not need to claim peer-review quality; it needs to make the next human review cheaper and more targeted.

## Error Handling

OpenAlex fetch failures should not corrupt the normalized corpus. Raw pages should be written only after successful responses. Failed pages should be recorded in a fetch log with URL, status, error, and retry count.

Network access may be unavailable in a sandbox. Scripts should support a cached mode that works with already downloaded pages, and the README should document when live fetch requires approval/network access.

The paper release gate should fail on malformed ledgers, missing required article files, unknown source IDs, and high-severity reviewer-audit findings. It should warn, not fail, when optional full-text PDFs are unavailable.

## Testing

Add focused tests for:

- OpenAlex normalization from a small fixture page;
- de-duplication of works across broad-topic and core-journal queries;
- literature map generation from normalized records;
- paper registration in `meta/papers.yml`;
- local publish output for the new paper;
- reviewer automation against the new paper ledger;
- site generation for the new paper and RAG page;
- date footnote presence in the new LaTeX front matter.

Tests should use fixtures and cached records, not live OpenAlex calls.

## Success Criteria

- The repo contains a new `papers/shovel-ready-trap/` paper with a full LaTeX draft, references, evidence ledger, workflow logs, and scripts.
- OpenAlex metadata for open-access regional science in the last five years can be fetched or rebuilt from cache.
- The manuscript presents a concrete regional-science contribution: project-pipeline conversion as a measurable mechanism in regional development.
- The paper is registered with `meta/`, publishes into `papers-out/`, and appears on the GitHub Pages site.
- Reviewer automation runs and produces dossiers, RAG artefacts, reviewer questions, adversarial audit, and release summary.
- The new paper has an SSRN package directory and an Overleaf status/check-in artefact.
- The first-page LaTeX date footnote is present.
