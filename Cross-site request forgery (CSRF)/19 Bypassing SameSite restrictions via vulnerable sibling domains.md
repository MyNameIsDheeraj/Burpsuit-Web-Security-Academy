# 19. Bypassing SameSite restrictions via vulnerable sibling domains

- **Whether you're testing someone else's website or trying to secure your own, it's essential to keep in mind:**
    - A request can still be **same-site** even if it's issued **cross-origin**.
- **Make sure you thoroughly audit all of the available attack surface**, including:
    - Any **sibling domains**.
- **In particular, be aware of vulnerabilities that enable you to elicit an arbitrary secondary request**, such as:
    - **XSS (Cross-Site Scripting)**, which can:
        - Compromise site-based defenses completely.
        - Expose **all of the site's domains** to cross-site attacks.
- **In addition to classic CSRF, remember:**
    - If the target website supports **WebSockets**, this functionality might be vulnerable to:
        - **Cross-Site WebSocket Hijacking (CSWSH)**.
            - This is essentially just a **CSRF attack targeting a WebSocket handshake**.
- **For more details:**
    - See our topic on **WebSocket vulnerabilities**.