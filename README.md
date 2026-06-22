# it-problem-solver

A Claude skill that brings structured, senior-engineer thinking to IT problem investigation. Built on the OHTV-D framework — Observe, Hypothesize, Test, Verify, Document — the same pattern used by SREs and infrastructure engineers in production environments.

Includes integrated token compression based on the [caveman](https://github.com/JuliusBrussee/caveman) philosophy, reducing output length by approximately 65% while preserving full technical accuracy.

---

## Why This Exists

Most AI-assisted debugging jumps straight to solutions before understanding the problem. This skill enforces a disciplined investigation process: gather facts first, form ranked hypotheses second, test with targeted commands third. It prevents the pattern of trying random fixes and hoping one works.

---

## What It Covers

The skill is domain-agnostic and has been tested across:

- Application development (Python, Node.js, Java, and others)
- Infrastructure and DevOps (Linux, Docker, Kubernetes)
- Databases (MySQL, PostgreSQL, Redis)
- Networking (DNS, TLS, firewall, connectivity)
- Security incident triage
- General IT support

---

## The Investigation Framework

Every session follows five phases:

**Observe** — Separate facts from assumptions. Identify scope, timeline, recent changes, and available artifacts (logs, traces, error codes).

**Hypothesize** — Form two to four ranked hypotheses based on evidence. Draws from a taxonomy of universal failure patterns: recent changes, resource exhaustion, dependency failure, race conditions, data corruption, environment drift, and capacity limits.

**Test** — Provide specific, executable steps to verify each hypothesis. Ordered from least invasive to most. Evidence is preserved before any system changes.

**Verify** — Confirm the root cause is identified, the fix resolves the original symptom, and no side effects were introduced.

**Document** — Produce a structured incident report with timeline, root cause, solution applied, and prevention actions.

---

## Caveman Mode

Activated with `/caveman`. Compresses Claude's responses while keeping all technical content exact — code, commands, error strings, and API names are never abbreviated.

```
/caveman        full mode (default)
/caveman lite   drop filler, keep full grammar
/caveman ultra  maximum compression, fragment style
stop caveman    return to normal prose
```

The compression automatically disables for security warnings, irreversible actions, and any step where ambiguity could cause harm.

Example of the same diagnosis at different verbosity levels:

```
Normal:  "The reason your service is not responding is most likely because
          the connection pool has been exhausted. I would recommend checking
          the current connection count and increasing the pool size."

Full:    "Connection pool exhausted. Check active conns, increase pool_size
          in config."

Ultra:   "Pool full. Check conns → up pool_size."
```

---

## Repository Structure

```
it-problem-solver/
├── SKILL.md
└── references/
    ├── diagnostic-commands.md
    └── error-pattern-library.md
```

`SKILL.md` contains the main framework. The two reference files are loaded on demand — diagnostic commands when specific platform commands are needed, error patterns when matching a known error signature.

---

## Installation

**Claude.ai**

Download `it-problem-solver.skill` from the releases page. Open Claude.ai, go to Settings, then Skills, and upload the file.

**Claude Code**

```bash
git clone https://github.com/YOUR_USERNAME/it-problem-solver
cp -r it-problem-solver ~/.claude/skills/
```

---

## Reference Files

`diagnostic-commands.md` covers Linux, Docker, Kubernetes, MySQL, PostgreSQL, Redis, Nginx, Apache, and Windows — roughly 50 commands organized by platform.

`error-pattern-library.md` covers Python, JavaScript/Node.js, Java, MySQL, PostgreSQL, Docker, Kubernetes, networking, Linux, and Git — roughly 60 named error patterns with likely causes and first investigation steps.

---

## Credits

Token compression approach adapted from [caveman](https://github.com/JuliusBrussee/caveman) by Julius Brussee (MIT).

OHTV-D framework adapted from SRE and incident response best practices.

---

## License

MIT
