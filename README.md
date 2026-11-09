# Incident response: "Locked Friday morning"

> **Ticket SOC-4471 — priority high**
> Friday, 08:40. The network team reports that **host** — a Linux server your
> team hardened last month during the Linux Security labs — made repeated
> outbound connection attempts to an external address overnight. The host still
> serves its usual report page and SSH still works, so nobody rebooted it.
> A finance deadline depends on this machine. **Decide whether it was
> compromised, and if so, how — before the 11:00 stand-up.**

You are the responder. You have a root console on the host and a copy of the
integrity baseline that was taken right after hardening ("known-good, restored
from backup"). The attacker, if there is one, has had hours on the box.

This is a **defensive** exercise. Nothing on the host is live malware; every
artefact is inert. Your job is to **find, explain and remediate**, then say what
would have stopped or caught it — not to attack anything.

## Start the host

```bash
# The instructor gives you INCIDENT_IMAGE (a digest-pinned reference).
export INCIDENT_IMAGE=...        # paste the value for your group
docker compose up -d
docker compose exec host bash    # your root console on the host
```

The clean integrity baseline is in [`baseline/`](baseline/). Restore it and
compare:

```bash
cp baseline/aide.db /var/lib/aide/aide.db
cp baseline/aide.conf /etc/aide/aide.conf
aide --config /etc/aide/aide.conf --check
```

## What to produce

Work the incident like a real one. Use the tools from the course — osquery,
AIDE, and standard system commands (`find`, `ss`, `awk`, `journalctl`/log
files). Fill in [`docs/REPORT-TEMPLATE.md`](docs/REPORT-TEMPLATE.md):

1. **Triage** — first five checks you run and why.
2. **Findings** — each suspicious artefact with the *command and output* that
   found it. Not every change is an attack: some are legitimate administration.
   Say which, and how you can tell.
3. **Entry and timeline** — how did they get in, and in what order did things
   happen? The authentication log tells a story.
4. **Remediation** — for each real finding: the fix, and a check proving it is
   gone.
5. **Risk delta** — for each confirmed artefact, which control from the hardening
   course (Phases 2–15) would have prevented or detected it? Finish with at most
   200 words: is this host trustworthy now, and what would you still not assume?

Submit one ZIP: the report plus your evidence files from `evidence/`.
See [`docs/CHECKLIST.md`](docs/CHECKLIST.md) for where to look. There is no list
of answers in this repository, and no write-ups — the point is to find them.

## Rules of engagement

- Stay on this host. Do not scan or connect to the address you find in the logs;
  it is a documentation-range placeholder and routes nowhere.
- Keep the container running while you work; don't recreate it, or you lose the
  live process evidence. A restart preserves the filesystem; `docker compose
  down` resets everything.
