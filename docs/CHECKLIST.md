# Where to look (no answers here — just the map)

Use these as prompts. Each points at a class of persistence or access that the
hardening course covered. Record the command and its output for anything you flag.

## Accounts and access (Phases 2, 4)
- [ ] Every account with UID 0 — should there be more than one?
- [ ] `authorized_keys` for each human user — does every key belong?
- [ ] sudo policy — any NOPASSWD or unexpected grant? (`sudo -ll`, `/etc/sudoers.d/`)

## Privileged files (Phase 5)
- [ ] SUID/SGID inventory vs your Phase 5 notes — anything new, or in an odd path?
- [ ] osquery `suid_bin`, or `find / -xdev -perm -4000 -type f`.

## Persistence (Phases 12, 14)
- [ ] Scheduled jobs: `/etc/cron.d/`, `/etc/cron.*`, user crontabs.
- [ ] Library preload: does `/etc/ld.so.preload` exist, and what is in it?
- [ ] Integrity: restore the baseline and run an AIDE check. Judge each diff —
      added, changed, or legitimately administered?

## Running state (Phase 15)
- [ ] Listening ports and their owning processes (osquery `listening_ports` +
      `processes`, or `ss -ltnp`). Any listener you cannot explain?
- [ ] For a suspicious process, check `/proc/<pid>/exe` — is its binary still on
      disk, or deleted?
- [ ] Top processes by memory; anything disguised as a system daemon?

## Story (auth log)
- [ ] Read `/var/log/auth.log`: brute force, the first success, what the account
      did next. Tie the entry point to what you found above.

## Judgement
- [ ] Separate the real compromise from routine administration and from changes
      the container runtime makes on boot. Say how you decided.
