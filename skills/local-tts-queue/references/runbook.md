# Local TTS Queue Runbook

## 1) Validate prerequisites
- Environment:
  - `ELEVENLABS_API_KEY`
  - `ELEVENLABS_VOICE_ID`
- Runtime:
  - `mpv` installed and executable

Quick checks:
```bash
printenv ELEVENLABS_API_KEY | wc -c
printenv ELEVENLABS_VOICE_ID | wc -c
command -v mpv
```

## 2) Validate queue plumbing
```bash
/home/brad/.openclaw/workspace/scripts/tts-queue-status.sh
```
Confirm queue file, lock file, and log path exist and are writable.

## 3) Smoke test end-to-end
```bash
/home/brad/.openclaw/workspace/scripts/speak-local-queued.sh "Queue smoke test"
```
Then monitor worker log for dequeue/synth/playback completion.

## 4) Worker failure triage
Common failures:
- Missing env vars: worker cannot synthesize
- Missing `mpv`: synth may succeed but playback fails
- Queue lock stale: queue appears stuck

Actions:
1. Fix missing dependency.
2. Restart daemon/worker.
3. Re-enqueue one test item.
4. Confirm queue drains.

## 5) Burst latency triage
If queue wait ramps quickly during bursts:
- Reduce or disable earcons in worker critical path.
- Enable/adjust burst coalescing window.
- Add stale-item TTL for superseded chatter.
- Consider prefetching next synth while current audio plays.

## 6) Policy checks
For protected users (Brad/RECTANGL):
- Use local speaker path only.
- Do not emit Discord TTS attachments as fallback.
