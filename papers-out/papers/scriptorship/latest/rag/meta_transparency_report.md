# Meta-Transparency Report

This report describes how the inspection layer was generated.

## Mechanical Checks

- validate_claims.py: passed (0s)
- check_latex_citations.py: passed (0s)
- check_methods_quality.py: passed (0s)
- check_data_artifacts.py: passed (1s)
- build_warrant_graph.py: passed (0s)
- source_bias_report.py: passed (0s)
- build_transparency_log.py: passed (0s)
- check_overclaiming.py: passed (0s)
- build_interrogation_index.py: passed (0s)
- build_claim_dossiers.py: passed (0s)
- build_source_dossiers.py: passed (0s)
- build_reviewer_question_bank.py: passed (0s)
- check_interrogation_costs.py: passed (0s)
- build_appendix_index.py: passed (0s)
- query_interrogation_index.py: passed (0s)
- ledger_ask.py: passed (0s)
- build_query_trace_report.py: passed (1s)
- check_adversarial_audit.py: passed (0s)

## Generated Outputs

- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/interrogation_index.json` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/rag_query_pack.json` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/claim_dossiers.md` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/source_dossiers.md` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/reviewer_question_bank.md` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/interrogation_cost_report.md` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/query_trace_report.md` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/appendix/adversarial_audit_report.md` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/workflow/logs/check_traces.jsonl` from generated
- `/Users/user/dev/scriptor-master/scriptor/papers/scriptorship/workflow/logs/interrogation_traces.jsonl` from generated

## Human Audit Required

- Human source reading remains required.
- Warrant levels are prototype judgements.
- The pipeline can check structure and provenance, not scholarly truth.

## What This Pipeline Cannot Verify

- Whether a source interpretation is substantively correct.
- Whether the argument is persuasive.
- Whether a future policy source has changed after the run date.
