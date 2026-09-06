# SSH Log Analyzer 🔐

A lightweight Python tool for analyzing Linux authentication logs and detecting repeated failed SSH login attempts.

The script scans authentication logs, extracts suspicious IP addresses, tracks failed login attempts within a configurable time window, and generates an alert when a specified threshold is exceeded.

## Features

* Reads Linux authentication logs line by line
* Detects failed SSH login attempts
* Extracts source IPv4 addresses
* Tracks repeated attempts from the same IP address
* Uses a configurable time window
* Uses a configurable alert threshold
* Supports common SSH authentication failure patterns
* Uses only the Python standard library

## Detected Log Patterns

The analyzer currently detects patterns such as:

* `Failed password`
* `Invalid user`
* `authentication failure`

Example:

```text
Sep 07 12:10:21 server sshd[1234]: Failed password for root from 192.168.1.50 port 55221 ssh2
```

## Requirements

* Python 3
* Linux authentication logs such as `/var/log/auth.log`

No external Python packages are required.

## Usage

Run the analyzer from the terminal:

```bash
python3 log_analyzer.py <log_file> <time_window_minutes> <threshold>
```
### Quick Test

You can test the analyzer using the included sample log file:

```bash
python3 log_analyzer.py examples/sample_auth.log 5 3
### Example

```bash
python3 log_analyzer.py /var/log/auth.log 5 3
```

This command checks the authentication log and generates an alert if the same IP address produces at least **3 failed login attempts within 5 minutes**.

## Example Output

```text
Uyarı: 192.168.1.50 adresinden son 5 dakikada 3 başarısız giriş (2026-09-07 12:15:03).
```

If the configured threshold is not exceeded:

```text
Uyarı yok: eşik aşılmadı.
```

## How It Works

1. The log file is read line by line.
2. Timestamps are extracted from syslog-style entries.
3. Regular expressions search for SSH authentication failures.
4. Source IP addresses are extracted from matching entries.
5. Failed attempts are grouped by IP address.
6. Old attempts outside the configured time window are removed.
7. An alert is generated when an IP reaches the configured threshold.

## Project Structure

```text
log_analyzer/
├── examples/
│   └── sample_auth.log
├── .gitignore
├── LICENSE
├── README.md
└── log_analyzer.py
```

## Use Cases

This project can be used as a simple introduction to:

* Linux log analysis
* SSH security monitoring
* Brute-force detection
* Regular expressions
* Python automation
* Basic cybersecurity monitoring

## Future Improvements

Possible improvements include:

* IPv6 support
* Command-line arguments with `argparse`
* JSON and CSV output
* Persistent alert logging
* IP whitelisting
* Configurable detection patterns
* GeoIP lookup
* Email or webhook notifications
* Automated tests
* Real-time log monitoring

## Disclaimer

This project is intended for educational and defensive security purposes.

## License

This project is licensed under the MIT License.
