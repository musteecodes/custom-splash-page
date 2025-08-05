# 🛠️ custom-splash-page

A custom HTML-based captive portal splash page designed for [NoDogSplash](https://github.com/nodogsplash/nodogsplash). This project includes a login form that integrates with NoDogSplash’s authentication system using the `auth.sh` script and built-in variables like `$authaction`, `$tok`, and `$redir`.

---

## 📁 Features

* Responsive HTML/CSS design
* Username and password login
* Token-based GET authentication
* Customizable icons and layout
* Integrates with `auth.sh` binary authentication

---

## 📂 Folder Structure

```
custom-splash-page/
├── index.html          # Splash page
├── README.md           
```

---

## 🚀 Setup Instructions

1. **Install NoDogSplash**

   Make sure `nodogsplash` is installed and active on your OpenWRT or Linux system.

2. **Add custom splash page**

   Copy `index.html`, `auth.sh`, and other files into the NoDogSplash directory:

   ```bash
   sudo cp index.html /etc/nodogsplash/htdocs/
   sudo cp auth.sh /etc/nodogsplash/htdocs/
   sudo chmod +x /etc/nodogsplash/htdocs/auth.sh
   ```

3. **Update configuration**

   Edit `/etc/nodogsplash/nodogsplash.conf` and enable binary authentication:

   ```
   bin_auth = 1
   bin_auth_path = /etc/nodogsplash/htdocs/auth.sh
   ```

4. **Restart NoDogSplash**

   ```bash
   sudo systemctl restart nodogsplash
   ```

---

## 🔧 HTML Form Variables

These variables are dynamically replaced by NoDogSplash:

* `$authaction` – the authentication handler URL
* `$tok` – session token
* `$redir` – URL to redirect user after login

Example form:

```html
<form action="$authaction" method="GET">
  <input type="hidden" name="tok" value="$tok">
  <input type="hidden" name="redir" value="$redir">
  <input type="text" name="username" placeholder="Username" required>
  <input type="password" name="password" placeholder="Password" required>
  <input type="submit" value="Log In">
</form>
```

---

## 🧠 Tips

* Log output with `sudo nodogsplash -d 2 -f` to debug
* Use `sha256sum` in `auth.sh` to hash passwords securely
* Ensure correct permissions and IP rules

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
