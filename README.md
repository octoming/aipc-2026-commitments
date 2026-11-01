# Hash commitments for a 2026 AI-generated philosophy essay pipeline

This repository contains no essay text, prompts or messages. It holds only SHA-256 commitments.

Every action of the pipeline (model calls, tool runs, selections, failures, refusals, human inputs and their gate verdicts) is an entry in a private, append-only, hash-chained log. Each entry's `hash` covers its full contents and the previous entry's hash (`prev`). As the run proceeds, the fields `writer, seq, time, action, hash, prev` of every entry are appended to `stream/<writer>.jsonl` here and pushed.

What this allows after the log is released:
- Anyone can recompute every entry hash from the released log and compare it with this stream. A changed, removed or reordered entry breaks the match.
- GitHub's server-side commit times bound when each entry already existed.
- Failed or discarded runs are entries too, so dropping one later would leave a visible gap in the chain.

What it does not prove: that an entry's content is true, or that no work happened entirely outside the logging system. Those are addressed elsewhere in the methodology (sealed model runner, clean-room checks and OpenTimestamps and RFC 3161 receipts).
