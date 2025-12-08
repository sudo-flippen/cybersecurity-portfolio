# Incident Report — Home Lab SOC Simulation

**Incident ID:** HLS-001
**Date:** 2025-12-08
**Reported by:** Logan Flippen

## Summary
Two HTTP captures performed:
1. Initial HTTP capture (headers only) — no GET shown.
2. Second HTTP capture (GET visible) — successful HTTP request capture.

## Tools Used
- Wireshark
- Terminal (curl, dig, nc)
- macOS

## Observations
- Headers captured include Host and User-Agent.
- Second capture shows GET request method successfully.
- Both captures saved as `.pcapng` files.

## Conclusion
This demonstrates the ability to capture HTTP traffic, analyze it, and document findings for a SOC analyst portfolio.