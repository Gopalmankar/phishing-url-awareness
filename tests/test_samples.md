# Test Results

Python version used: 3.14.4 | Operating system: Windows | Date: 29-10-2026

| # | Input | Expected result | Actual result | Pass/Fail |
|---|-------|-----------------|---------------|-----------|
| 1 | `https://www.example.com/login` | No listed warning signs | No listed warning signs found. This does NOT prove safety. | PASS |
| 2 | `http://192.0.2.10/account` | IP address + HTTP | Uses an IP address instead of a familiar domain. Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 3 | `http://example.com@sample.invalid/login` | @ symbol + HTTP | Contains an @ symbol; inspect carefully. Uses HTTP. HTTPS alone does not prove trust. | PASS |
| 4 | `https://a.b.c.d.e.example.invalid/path` | Many hostname segments | Contains many hostname segments/subdomains. | PASS |
| 5 | `https://xn--example.invalid/` | Punycode-style hostname | Contains a punycode-style hostname. | PASS |


## Notes

I learned that a URL has parts (scheme, hostname, path) and that the hostname is the most important part to read. The `@` test showed me that `http://example.com@sample.invalid/login` really points to `sample.invalid`, not `example.com`.

What surprised me was that `https://www.example.com/login` showed no warning signs, yet the program says this does NOT prove safety. Warning signs are only clues, not proof.

I also learned that handling empty input and adding a loop with `q` to quit made testing much faster, and I re-ran all five tests after adding my improvements to make sure nothing broke.

