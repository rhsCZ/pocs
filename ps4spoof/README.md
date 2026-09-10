# PS4 Address-Bar Spoofing via Uncommitted Navigation

This vulnerability were discovered with [V12](https://v12.sh) by [Renwa](https://x.com/RenwaX23) of the [V12 security team](https://x.com/v12sec).

## Proof of Concept

- A live PoC is available at **[https://ps4spoof.v12.sh](https://ps4spoof.v12.sh)**.
- `poc.html` inside this repo.

## Summary

The PlayStation 4 web browser contains an **address-bar spoofing vulnerability** that allows an attacker-controlled page to remain visible while the browser displays the URL of a trusted website.

The PoC opens an `about:blank` window and writes a fake Google login page into it. It then repeatedly navigates the window to `https://www.google.com:81`, an endpoint intended to remain unreachable or loading.

The PS4 browser updates its address bar using this pending destination but fails to replace the attacker-controlled document. As a result, the victim sees a Google hostname in the address bar while viewing content created entirely by the attacker.

## Attack Flow

1. The victim opens the attacker’s page in the PS4 browser.
2. The victim selects the “Sign in with Google” button.
3. The page opens an `about:blank` window and injects a simulated login form.
4. The window begins navigating to `https://www.google.com:81`.
5. The address bar shows the Google URL while the fake login page remains visible.
6. Credentials entered into the form can be sent to an attacker-controlled server.

## Impact

This vulnerability can be used to create convincing phishing pages that impersonate Google, Sony, banks, email providers, or other trusted services.

## Affected

- **Product:** PlayStation 4 Web Browser
- **Firmware versions:** Latest
- **Patch status:** Unpatched
