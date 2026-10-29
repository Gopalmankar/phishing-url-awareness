# EWB Phishing URL Awareness Checker

## Overview
Phishing is a trick where criminals send fake links or messages to make people share passwords, card numbers or OTPs. This project is a small Python command-line tool that reads the text of a URL and points out selected warning signs. It only inspects the text. It never opens or visits the URL.

## Features
- Detects an @ symbol in the URL
- Flags unusually long URLs (over 100 characters)
- Flags IP-address hostnames
- Flags many hostname segments (5 or more)
- Flags punycode-style hostnames (xn--)
- Flags the HTTP scheme
- Loop mode: check several URLs in one run, type q to quit
- "REVIEW CAREFULLY" summary with the number of warning signs found

## Requirements
Python 3.10 or later. No extra packages.

## How to Run
Windows: `py phishing_checker.py` (or `python phishing_checker.py`)

Mac/Linux: `python3 phishing_checker.py`

## Example Output
```
EWB Phishing URL Awareness Checker
Text checks only - this program does not open URLs.

Enter a sample URL (or type q to quit): http://192.0.2.10/account

Result:
- Uses an IP address instead of a familiar domain.
- Uses HTTP. HTTPS alone does not prove trust.

REVIEW CAREFULLY: 2 warning sign(s) found.
Never enter passwords from unexpected links.

Enter a sample URL (or type q to quit): q
Goodbye! Stay alert online.
```

## Testing
Full table is in `tests/test_samples.md`.

| # | Input | Expected | Actual | Result |
|---|-------|----------|--------|--------|
| 1 | `https://www.example.com/login` | No warning signs | No listed warning signs found. This does NOT prove safety. | PASS |
| 2 | `http://192.0.2.10/account` | IP address + HTTP | IP address and HTTP warnings shown | PASS |
| 3 | `http://example.com@sample.invalid/login` | @ symbol + HTTP | @ symbol and HTTP warnings shown | PASS |
| 4 | `https://a.b.c.d.e.example.invalid/path` | Many hostname segments | Many hostname segments warning shown | PASS |
| 5 | `https://xn--example.invalid/` | Punycode-style hostname | Punycode-style hostname warning shown | PASS |

## Screenshots
![Sample run](screenshots/sample_run.png)
![Test results](screenshots/test_results.png)

## Improvements
1. **Loop with quit** - Earlier the program checked only one URL and then closed. I replaced the single input with a `while True` loop, so I can check many URLs in one run. Typing `q`, `quit` or `exit` stops the loop. I chose it because it makes testing faster. I tested it by entering several URLs one after another, then an empty input, then `q`, and the program ended with "Goodbye!".
2. **"Review carefully" summary** - I added a helper function `has_warnings()` that separates real warnings from information messages such as "No URL entered". When real warnings are found, the program prints "REVIEW CAREFULLY" with the number of warning signs. I tested it: it appeared for `http://192.0.2.10/account` (2 warnings), and it did not appear for `https://www.example.com/login` or for empty input.

## Limitations
This is an educational tool. It only reads URL text. It does not visit
URLs, scan for malware or prove that a URL is safe. No warning signs
found does NOT mean a URL is safe.

## Ethical Use
Use sample strings only. Do not collect credentials. Do not use this
project to deceive anyone or to test websites without permission.

## Author
Gopal Mankar, AI POWERED CYBERSECURITY INTERNSHIP, EWB Courses