Vagrant.configure("2") do |config|
  config.vm.define "centos7" do |centos|
    centos.vm.box = "centos/7"
    centos.vm.box_version = "2004.01"
    centos.vm.network "private_network", type: "dhcp"
    centos.vm.provision "shell", inline: <<-SHELL
      #!/bin/bash
      # Variables
      USERNAME="test"
      PASSWORD="test123"

      # Create the user
      useradd $USERNAME

      # Set the password for the user
      echo "$USERNAME:$PASSWORD" | chpasswd

      echo "User $USERNAME created with sudo privileges and password: $PASSWORD"
    SHELL
  end
  
  config.vm.define "windows" do |win|
    win.vm.box = "gusztavvargadr/windows-server"
    win.vm.box_version = "2102.0.2409"
    win.vm.network "private_network", type: "dhcp"
    win.vm.communicator = :winrm
    win.winrm.username = "test"
    win.winrm.password = "test"
    win.winrm.port = 5985
    win.winrm.transport = :plaintext
    win.vm.provision "shell", inline: <<-SHELL
        echo "Configuring WinRM Listener"

        # Enable WinRM
        winrm quickconfig -force

        # Set WinRM to allow unencrypted connections (optional, only for testing)
        Set-Item WSMan:\localhost\Service\AllowUnencrypted -Value $true

        # Create a WinRM listener on HTTP (port 5985)
        New-NetFirewallRule -Name "WINRM-HTTP-In-TCP" -DisplayName "WINRM HTTP" -Enabled True -Protocol TCP -Action Allow -Direction Inbound -LocalPort 5985

        # Create a WinRM listener on HTTPS (port 5986)
        # Uncomment the next lines to enable HTTPS
        # New-Item -Path WSMan:\localhost\Listener -SelectorSet @{Address="*";Transport="HTTPS"} -Value @{CertificateThumbprint="YOUR_CERT_THUMBPRINT"}
        # New-NetFirewallRule -Name "WINRM-HTTPS-In-TCP" -DisplayName "WINRM HTTPS" -Enabled True -Protocol TCP -Action Allow -Direction Inbound -LocalPort 5986

        # Restart WinRM service
        Restart-Service WinRM
      SHELL
  end
end
