# Hey, I'm SillyZir 👋

### Autonomous Software Engineering · Agent Evaluation · Systems Reliability

I build autonomous systems that do real technical work — and I spend most of my effort proving
their output is right.

---

## 🤖 Agent Omega

An autonomous repair system for open-source Go projects. It reads a bug report, locates the
responsible code, writes a patch, generates a regression test, and clears two independent automated
reviews and 15 release gates before anything ships.

Source is private. These are the public results.

| Merged upstream | What it fixes |
|---|---|
| [caddy #7916](https://github.com/caddyserver/caddy/pull/7916) | isolate active health-check state per distinct check config |
| [go-ethereum #35433](https://github.com/ethereum/go-ethereum/pull/35433) | only synthesize finalized/safe markers with an explicit sync target |
| [rclone #9726](https://github.com/rclone/rclone/pull/9726) | reuse resumable-upload chunk buffers via a size-matched pool |
| [caddy #7904](https://github.com/caddyserver/caddy/pull/7904) | isolate auth provider responses to prevent cross-provider clobbering |
| [caddy #7920](https://github.com/caddyserver/caddy/pull/7920) | shield specific hostnames from a covering wildcard's client auth |

**Nine patches merged** across caddy, rclone, and go-ethereum — concurrency isolation, buffer
reuse, and protocol correctness, each reviewed by that project's maintainers.

---

## 📏 How it's measured

I built a benchmark from **37 real bugs with known answers**, each paired with the fix maintainers
actually merged.

| | Correct file ranked first |
|---|---|
| Keyword baseline | **4 / 37** |
| Agentic localization | **29 / 37** |

Four agent runs exhausted their turn budget and produced no ranking. They're counted as misses, so
both numbers share a denominator.

On patch generation, of 35 issues that produced a patch: **28 touch a correct file**, **25 land
within ±5 lines** of the human-changed region. An LLM judge calls 17 of 35 root-cause equivalent —
but a blinded audit of that judge found it models test adequacy and scope *not at all*, so I treat
it as a research proxy, not a claim that those patches were ready to merge.

That same benchmark is what killed my first version. A second implementation of the verifier in
Rust was measured against its own pre-registered bars, failed them, and was not promoted — the
result stayed in the record instead of being retried until it passed.

---

## ⚙️ The design constraint

The objective isn't generating code. It's an autonomous system that performs useful engineering
work while staying **measurable · constrained · auditable · recoverable**:

- Pass criteria registered before results exist; test data frozen
- 15 auto-ship gates, each tested by feeding it deliberately broken patches to confirm it rejects them
- Two independent automated reviewers with disagreement detection
- Fail-closed evidence capture — an unverifiable run halts rather than proceeding
- Full autonomy enabled for two repositories; everything else requires operator approval

---

**Working in:** Python · Go · Rust · Gno
**Interested in:** autonomous software engineering, agent evaluation, developer tooling, reliability
and failure recovery, human/AI collaboration
