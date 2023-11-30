- Apps and Features → optional Features
  - OpenSSH client
  - OpenSSH server
- powershell as administrator
  ```jsx
  # check
  Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

  # Install
  Add-WindowsCapability -Online -Name OpenSSH.Server ... 0.0.1.0

  # Uninstall
  Remove-WIndowsCapability -Online -Name OpenSSH.Server ... 0.0.1.0
  ```
