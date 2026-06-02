# Benchmarks — baseline & regression protocol

`baseline.md` holds the committed reference numbers for TextDiff.Sharp's
performance benchmarks. It is the comparison point shown in the manual
`benchmark.yml` workflow's job summary.

## How to produce / update the baseline

The committed baseline MUST come from the GitHub Actions runner (ubuntu-latest),
so that it is comparable to what `benchmark.yml` measures. Do NOT commit numbers
measured on a local developer machine.

1. Run the manual workflow on GitHub:

       gh workflow run benchmark.yml

2. Open the workflow run's job summary and copy the "Current run"
   `*-report-github.md` tables.
3. Paste them into `baseline.md`, replacing the PENDING block, and fill the
   header (date, commit SHA, runner).
4. Commit `baseline.md` in the same PR as any change that intentionally altered
   performance, so reviewers see the delta.

A local run is fine for ad-hoc sanity checks (not for the committed baseline):

    dotnet run -c Release --project src/TextDiff.Sharp.Benchmarks -- --filter "*" --exporters github

## When to update baseline.md

Update **only** when a performance change is intended and reviewed.

CI (`ci.yml`) does **not** run benchmarks (build/test only) and never uploads
artifacts — per the repository's GitHub Actions resource policy.
