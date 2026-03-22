# Security Policy

## Scope

This repository contains a Claude Code skill -- a set of markdown instructions that guide AI-assisted server management. It does not contain executable code, API keys, or credentials.

## Reporting a Vulnerability

If you discover a security concern (e.g., commands that could weaken server security, outdated cryptographic recommendations, prompt injection risks, or instructions that could cause Claude to expose sensitive data), please report it responsibly:

1. **Do not** open a public issue
2. Email the maintainer or open a private security advisory via GitHub
3. Include a clear description of the concern and steps to reproduce

## What Counts as a Security Issue

- Commands or configurations that weaken server security (e.g., overly permissive firewall rules, weak cipher suites)
- Outdated hardening advice that no longer reflects best practices
- Instructions that could cause Claude to expose user credentials, SSH keys, or API keys
- Prompt injection patterns embedded in templates or examples
- Content that could cause Claude to bypass safety guidelines or skip confirmation for destructive commands
- Deprecated cryptographic algorithms still recommended in the skill

## Response

We aim to acknowledge security reports within 48 hours and resolve confirmed issues within 7 days.
