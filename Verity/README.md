# Verity — AI Reliability Lab

A deployable, browser-local MVP for testing model responses against an inspectable starter benchmark. It works without Kytte or NVIDIA access.

## Use

1. Export the prompts from the site. Run each prompt in a fresh conversation with your model, retaining the same model settings.
2. Download the response template and fill its `responses` values with verbatim outputs, or enter responses directly in the site.
3. Import the JSON file, name the build, and run evaluation.
4. Inspect each check's reference and rationale. Save runs on your device to compare builds; export reports for a durable record.

The 12 original examples cover grounding, abstention, reasoning, and faithfulness. They are a small demonstration suite, not a statistically validated or representative benchmark. Agreement is not a hallucination-free score. Format deviations are unresolved review cases, and blanks are missing. Only the full reference answer passes after case and outer-whitespace normalization.

## Development

Node 20+; no dependencies. `npm test` runs the grading and import-validation tests. `npm run dev` serves http://127.0.0.1:4317. Deploy `dist/` as static assets; Sites identity is in `.openai/hosting.json`. All application assets are local, with no external fonts or analytics.

## Scope and privacy

- No model API calls, automatic natural-language fact checker, runtime interception, or remediation.
- Files are read in the browser. Saving a run stores answers in browser localStorage; JSON reports include the answers. No application database or account system is present.
- A handcrafted demo is visibly labeled, including in exported and saved reports.
- The independent working brand does not assert affiliation with Kytte, NVIDIA, or the cited researchers.

## Production path

1. Validate demand with a narrow use case, such as support-agent answers grounded in customer documentation. Recruit model builders to supply representative held-out test examples and expert labels.
2. Add a server-side endpoint that calls an allowlisted model provider. Keep keys in server secret storage, never browser code; add user authentication, quotas, request timeouts, and separated tenant storage.
3. When NVIDIA access is available, integrate a selected Nemotron model as an optional evidence-grounded judge. Require structured verdicts and evidence spans, represent unavailable evidence as uncertain, and isolate judged content from judge instructions. Treat the judge as fallible.
4. Measure judge precision/recall and agreement against independent human labels before displaying semantic risk metrics. Track abstention, coverage, runtime errors, latency, model and prompt versions, and cost separately.
5. Add custom suites, repeat runs, regressions on a shared test set, confidence intervals with a justified sampling design, and CI release checks. Keep runtime remediation as a separate future product capability.

Possible commercial direction: free small evaluations to establish trust, then paid private domain suites, team history, and CI regression checks. Pricing and willingness to pay remain unvalidated.

## References

Sun et al. (2024), *AI hallucination: towards a comprehensive classification of distorted information in artificial intelligence-generated content*, https://www.nature.com/articles/s41599-024-03811-x. The paper offers a taxonomy; it does not validate this implementation.

Kytte's description of its runtime reliability work: https://kytte.ai/blog/kytte-nvidia-nemotron-millisecond-reliability. Verity currently evaluates saved responses rather than operating inside agent execution.
