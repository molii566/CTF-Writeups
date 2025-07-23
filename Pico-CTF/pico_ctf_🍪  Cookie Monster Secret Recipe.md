## 🧠 picoCTF - Detailed Writeups by [Z4B0](https://www.linkedin.com/in/mahamud-abdirahman-151493375/)

### 🍪 Cookie Monster Secret Recipe

**Objective:** Discover a hidden flag embedded as a cookie value and decode it.

**Target URL:** `http://verbal-sleep.picoctf.net:50164`

**Tools & Resources:**

- Web browser with developer tools
- Base64 decode utility (`base64` CLI or online)

**Walkthrough:**

1. **Inspect Website**

   - Open the page and press `F12` to open Developer Tools.
   - Navigate to the "Application" (Chrome) / "Storage" (Firefox) tab to view cookies.

2. **Locate Secret Cookie**

   - Found cookie named `secret_recipe` with value:
     ```
     cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzX0RFN0E1RTc2fQ%3D%3D
     ```
   - URL-decoded (percent-decoding) yields the Base64 string:
     ```
     cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzX0RFN0E1RTc2fQ==
     ```

3. **Decode Base64**

   - Using CLI:
     ```bash
     echo 'cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzX0RFN0E1RTc2fQ==' | base64 -d
     ```
   - Reveals:
     ```
     picoCTF{c00k1e_m0nster_l0ves_c00kies_DE7A5E76}
     ```

4. **Submit Flag**
   - Enter the decoded string into the picoCTF flag submission form.

**Final Flag:**

```
picoCTF{c00k1e_m0nster_l0ves_c00kies_DE7A5E76}
```

---
