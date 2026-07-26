# Sources and synthesis notes

Generated: 2026-07-26

## Ranking methodology

GitHub does not expose a universal per-repository “downloads in the last seven days” metric for Agent Skills. This synthesis therefore used the nearest public adoption signals available at creation time:

1. skills.sh install telemetry and Hot/Trending listings;
2. cumulative skill installs shown by skills.sh;
3. GitHub repository activity and relevance;
4. direct functional similarity to video analysis, editing, generation, or rendering.

The result is a curated functional top five, not a mathematically exact seven-day download ranking.

## Five principal inspirations

1. **guimatheus92/mcp-video-analyzer — video**
   - Multi-platform ingestion, transcript extraction, keyframes, OCR, metadata, moment-level analysis.
   - Source: https://github.com/guimatheus92/mcp-video-analyzer

2. **video-db/skills**
   - Server-side ingest, understanding, search, editing, streaming, and video knowledge workflows.
   - Source: https://github.com/video-db/skills

3. **calesthio/openmontage — video-edit**
   - Deterministic local FFmpeg/ffprobe editing and reproducible commands.
   - Source: https://github.com/calesthio/openmontage

4. **remotion-dev/skills — remotion-best-practices / remotion-render / remotion-captions**
   - Component-driven video authoring, rendering, captions, and production validation.
   - Source: https://github.com/remotion-dev/skills

5. **heygen-com/hyperframes — hyperframes family**
   - HTML/CSS/GSAP video composition, lint/inspect/render workflow, deterministic motion graphics.
   - Source: https://github.com/heygen-com/hyperframes

## Additional references reviewed

- https://github.com/martinopiaggi/summarize
- https://github.com/kennyzheng-builds/seek-and-analyze-video
- https://github.com/aiagentwithdhruv/skills
- https://github.com/google-gemini/gemini-skills
- https://github.com/inference-sh/agent-skills
- https://github.com/coreyhaines31/marketingskills

## Synthesis policy

`video-studio-pro` is an original routing and workflow skill. It does not vendor source code, API credentials, model weights, or proprietary assets from the projects above. It combines publicly documented workflow ideas into one tool-aware operating contract and preserves attribution here.

External services are optional. The skill prefers local deterministic tools where possible and requires explicit user authorization before uploading private media to third-party APIs.
