## **README for XssDump**

### Overview

**XssDump** is a Python-based XSS (Cross-Site Scripting) vulnerability scanner designed to test web applications for potential XSS vulnerabilities. The script performs automated testing by injecting payloads into URLs and analyzing HTTP responses to check for the presence of malicious scripts.

- **Author**: Hackfut
- **Contact**: [t.me/HackfutSec](https://t.me/HackfutSec)
- **GitHub**: [https://github.com/HackfutSec/XssDump.git](https://github.com/HackfutSec/XssDump.git)
- **License**: MIT
- **Warning**: The author is not responsible for how this tool is used. Use it ethically and legally.

---

### Features

- **Multithreaded**: Utilizes Python's `ThreadPoolExecutor` for fast parallel processing, allowing multiple URLs to be tested at the same time.
- **Customizable Payload Injection**: Loads a list of XSS payloads from a JSON file to test for vulnerabilities.
- **Error Logging**: Automatically logs errors, such as failed HTTP requests, in a separate `errors.log` file.
- **Output**: The results of the scan are saved to an `XSS.txt` file, detailing all URLs found to be vulnerable.
- **Supports Different URL Structures**: Offers two options for URL sanitization—keeping the original URL or replacing the URL query parameter with `?id=`.
- **Configurable Thread Count**: Allows the user to specify the number of threads (workers) for testing, providing flexibility depending on the system's performance.

---

### Requirements

- Python 3.x
- Requests module (`pip install requests`)

---

### Installation

To use XssDump, follow these steps:

1. Clone the repository:

   ```bash
   git clone https://github.com/HackfutSec/XssDump.git
   cd XssDump
   ```

2. Install the required Python libraries (if you haven't already):

   ```bash
   pip install requests
   ```

3. Download or create a list of XSS payloads in a `xss_payloads.json` file. This file should contain the payloads you wish to use to test for vulnerabilities.

---

### Usage

1. **Run the Script**:

   In the terminal, navigate to the directory where `XssDump.py` is located and run the script:

   ```bash
   python XssDump.py
   ```

2. **Choose Testing Mode**:

   When prompted, choose between testing a single URL or a list of URLs:

   ```plaintext
   [✓] Do you want to test:
   
   (1) single URL
   (2) list of URLs
   ```

   - **Option 1**: Test a single URL.
   - **Option 2**: Test a list of URLs (provided via a file).

3. **Provide URLs**:

   - For **single URL testing**, enter the URL directly when prompted.
   - For **list of URLs**, provide the path to a file containing a list of URLs to test (one URL per line).

4. **Select a URL Testing Option**:

   Choose between two sanitization options for the URLs:

   ```plaintext
   1: Keep URL
   2: Replace with ?id=
   ```

   - **Option 1**: The script keeps the original URL structure and adds XSS payloads to the existing query parameters.
   - **Option 2**: The script modifies the URL to use `?id=` as the query parameter, and payloads are appended to this parameter.

5. **Enter Custom Parameter (optional)**:

   If you chose **Option 1** above, you will be asked to enter a parameter name, which will be used to inject the payload.

6. **Set Number of Threads**:

   Specify how many threads the script should use for testing. The default is 10 threads, but you can adjust this based on your system's capacity.

7. **Scanning**:

   The script will then proceed with the scan, injecting each payload into the URLs and checking for potential XSS vulnerabilities.

   - Vulnerable URLs are printed with a `[Vuln]` label.
   - Non-vulnerable URLs are printed with a `[Not Vuln]` label.

8. **Results**:

   - Vulnerable URLs are saved to an `XSS.txt` file.
   - Errors (e.g., failed HTTP requests) are logged in `errors.log`.

---

### Example

```plaintext
[✓] Do you want to test:

(1) single URL
(2) list of URLs

[<<] Choose (1/2): 1

[✘] Enter the single URL to test: http://example.com/search?q={payload}

[✓] Choose option:

1: Keep URL
2: Replace with ?id=

[<<] Your choice: 1

[] Enter you parameter: q

[✓] Number of Threads (default 10): 10

Scanning...
```

**Output Example**:

```plaintext
[>>] http://example.com/search?q=<script>alert(1)</script> --> [Vuln]
[x] http://example.com/search?q=invalidparam --> [Not Vuln]
```

---

### Output Files

- **XSS.txt**: Contains a list of URLs identified as vulnerable to XSS attacks.
- **errors.log**: Logs HTTP request errors, such as timeouts, connection issues, or other failures.

---

### Important Notes

- **Ethical Use**: Only scan websites you have explicit permission to test. Unauthorized scanning can be illegal and unethical.
- **Payloads**: The script uses predefined XSS payloads located in the `xss_payloads.json` file. You can customize this file with your own payloads if needed.

---

### Troubleshooting

- **Error: Payload file not found**  
  Ensure that the `xss_payloads.json` file exists in the same directory as the script.

- **Error: Invalid input for number of threads**  
  The number of threads must be a positive integer.

- **Error: URL list file does not exist**  
  Make sure that the file path for the list of URLs is correct.

---

### Contributing

Feel free to fork the repository, submit issues, or create pull requests if you wish to contribute improvements or fixes.

---

### License

This tool is open source and released under the **MIT License**.

--- 

**Disclaimer**: The author is not responsible for any misuse of this tool. Use it responsibly and legally.
