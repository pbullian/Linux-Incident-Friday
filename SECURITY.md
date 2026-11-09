# Security / content notice

This repository is **educational course material** for the 4IRC Linux Security
module at **CPE Lyon** (instructor: Pablo E. Bullian). It is the student side of a
graded incident-response practical ("TP"). If you are a scanner, reviewer, or
reader who landed here out of context, please read this before flagging.

## What this is

A **defensive** blue-team exercise. Students are given a Linux host that was
*deliberately prepared* for the lab and must **detect, explain and remediate** the
changes on it, then write an incident report. The learning objective is forensics
and incident response, not offense.

## What this is not

- **Not malware.** The lab image contains inert teaching markers only. Nothing in
  it is a functional backdoor, exploit, implant, or command-and-control client.
- **Not an attack.** There is no exploit code and nothing that attacks another
  system. The example "beacon" in the scenario only appends a line to a local log
  file; it makes no network connection. Any IP address shown is in the reserved
  **RFC 5737 documentation range** (`203.0.113.0/24`), which is non-routable.
- **Not for real use.** Do not deploy the lab image, run it in production, or use
  anything here on a system you do not own. It has no purpose outside the classroom.

## This repository contains no answers

There is no list of the planted artefacts and no write-up here, by design — the
exercise is to find them. The solution key is kept privately by the instructor.

## Contact

Questions about this material: the course instructor at CPE Lyon.
