## 1. Create *Certificate Authority* for code signing using *Keychain Access*.

[Steps to create certificate authority for code signing using keychain access](https://www.notion.so/Steps-to-create-certificate-authority-for-code-signing-using-keychain-access-ec28fc81280c4a6b8460a860c8286844?pvs=21)

## 2. Create code signing certificate using *Keychain Access*.

https://www.simplified.guide/macos/keychain-cert-code-signing-create

## 3. Launch terminal app.

## 4. Install *Xcode Command Line Tools* if not already installed.

```bash
$ xcode-select --install
```

## 5. Locate location or path of *PHP* module from *Apache*'s *PHP LoadModule* directive.

```bash
$ find -L /etc/apache2 -type f -print0 | xargs -0 grep -i "^loadmodule.*php"
/etc/apache2/other/00-httpd.conf:LoadModule php_module /opt/homebrew/opt/php/lib/httpd/modules/libphp.so
```

## 6. Sign *PHP* module using *codesign* with the code signing certificate name you've created.

```bash
$ codesign --sign "Mohd Shakir" --force --keychain ~/Library/Keychains/login.keychain-db /opt/homebrew/opt/php/lib/httpd/modules/libphp.so
```

## 7. Open *Apache* configuration file with *PHP LoadModule* directive using your preferred text editor.

```bash
$ sudo vi /etc/apache2/other/00-httpd.conf
```

## 8. Add code signing certificate name after module path in *PHP LoadModule* directive.

```bash
LoadModule php_module /opt/homebrew/opt/php/lib/httpd/modules/libphp.so "Mohd Shakir"
```

## 9. Restart *Apache* for changes to take effect.

```bash
$ sudo apachectl -k restart
```
