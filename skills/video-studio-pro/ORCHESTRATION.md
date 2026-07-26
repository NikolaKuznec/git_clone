# Video Studio Pro — Three-Agent Orchestration

## Purpose

Этот протокол превращает Skill в управляемый конвейер из трёх независимых ролей:

1. **Research Agent** — исследует и планирует.
2. **Build Agent** — создаёт воспроизводимый результат.
3. **Review Agent** — независимо проверяет и принимает либо возвращает на исправление.

Агенты могут выполняться отдельными процессами в поддерживающей multi-agent среде или последовательно одним агентом с жёстким переключением ролей и файловыми handoff-контрактами.

## State machine

```text
REQUEST
  ↓
RESEARCH
  ├─ blocked → USER_REPORT
  └─ ready
       ↓
BUILD
  ├─ blocked → USER_REPORT
  └─ rendered
       ↓
REVIEW
  ├─ pass → DELIVER
  ├─ revise → BUILD (maximum 2 cycles)
  └─ blocked → USER_REPORT
```

## Shared project layout

```text
project/
  source/
  assets/
  artifacts/
    research-report.json
    edit-decision-list.json
    build-manifest.json
    qa-report.json
    render-command.txt
    captions.srt
    preview.mp4
    final.mp4
    checksums.txt
  logs/
  cache/
```

## Orchestrator contract

### Step 1 — Intake

Normalize the request into:

```json
{
  "goal": "",
  "source": "",
  "target_platform": "",
  "deliverables": [],
  "constraints": {
    "privacy": "local-only|external-allowed",
    "budget": null,
    "deadline": null,
    "max_revision_cycles": 2
  }
}
```

### Step 2 — Dispatch Research Agent

Research Agent must produce a valid `research-report.json`. The orchestrator rejects the handoff when required provenance, timecodes, uncertainties or tool inventory are missing.

### Step 3 — Dispatch Build Agent

Build Agent receives the immutable research report. Any material deviation from the proposed plan must be recorded in `build-manifest.json` with a reason.

### Step 4 — Dispatch Review Agent

Review Agent receives all source-independent evidence needed to check the output. It must inspect the actual files and may not approve based only on Build Agent prose.

### Step 5 — Controlled revision

For `revise`, the orchestrator passes only `required_fixes` to Build Agent. Research is repeated only when the review discovers a factual/content problem, not for a purely technical render defect.

### Step 6 — Delivery

Deliver only outputs listed under `verified_outputs` in `qa-report.json`. Include:

- final paths;
- technical summary;
- quality score;
- known limitations;
- exact uncompleted steps;
- reproducibility command or manifest.

## Parallelism

Safe parallel work:

- transcription and scene detection;
- OCR on already-selected frames;
- audio analysis and visual metadata extraction;
- independent platform-format checks.

Unsafe parallel work:

- multiple writes to the same output;
- final render before EDL approval;
- QA before final file checksum is stable;
- two agents changing the same manifest.

## Failure policy

- Never fabricate a successful command or output.
- Preserve partial artifacts after failure.
- Report missing tools and exact installation commands.
- Do not retry an identical failed expensive operation without changing a relevant parameter.
- Stop external API use when its configured budget is reached.
- Never bypass DRM, authentication or access controls.

## Invocation template

```text
Use video-studio-pro in three-agent mode.
Research Agent: inspect the source, create evidence-backed research-report.json.
Build Agent: follow the accepted report, create reproducible preview/final artifacts and build-manifest.json.
Review Agent: independently inspect actual outputs, score them, and issue pass/revise/blocked in qa-report.json.
The orchestrator may run at most two revision cycles and must deliver only verified files.
```
