## 🧠 picoCTF - Detailed Writeups by [Z4B0](https://www.linkedin.com/in/mahamud-abdirahman-151493375/)

---

### 🔓 Hashcrack

**Objective:** Crack consecutive hashes served by a netcat service to reveal a final flag.

**Target:** `verbal-sleep.picoctf.net` on port `51759`

**Tools & Resources:**

- `nc` (netcat) for connecting to the remote service
- Local hash-cracking utilities: `hashcat` or `john the ripper`
- Online hash databases as fallback

**Walkthrough:**

1. **Connect to the service**

   ```bash
   nc verbal-sleep.picoctf.net 51759
   ```

   - Service responds with an MD5 hash prompt.

2. **MD5 Hash Cracking**

   - **Hash:** `482c811da5d5b4bc6d497ffa98491e38`
   - Attempt using `hashcat`:
     ```bash
     hashcat -m 0 482c811da5d5b4bc6d497ffa98491e38 wordlist.txt
     ```
   - Result: `password123`
   - Submit `password123` into the prompt to receive the next challenge.

3. **SHA-1 Hash Cracking**

   - **Hash:** `b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3`
   - Crack with `hashcat -m 100` or `john`:
     ```bash
     hashcat -m 100 b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3 wordlist.txt
     ```
   - Revealed password: `letmein`
   - Submit to get the final hash.

4. **SHA-256 Hash Cracking**
   - **Hash:** `916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745`
   - Use `hashcat -m 1400`:
     ```bash
     hashcat -m 1400 916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745 wordlist.txt
     ```
   - Found password: `qwerty098`
   - On submitting, the service prints the final flag.

**Final Flag:**

```
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_ce730f64}
```

---
