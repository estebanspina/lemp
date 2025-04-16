# Vagrant LEMP Environment on AlmaLinux 9

This repository contains a Vagrant configuration for setting up a LEMP (Linux, Nginx, MySQL/MariaDB, PHP) environment using AlmaLinux 9. This setup is ideal for development purposes.

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- [Vagrant](https://www.vagrantup.com/downloads)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Vagrant Configuration

The Vagrant configuration is defined in the Vagrantfile. Here are the key settings:

Base Box: AlmaLinux 9
Hostname: development.local
Network Configuration:
- Forwarded Port: Host port 8080 mapped to guest port 80
- Private Network: IP address 192.168.56.10
Resource Allocation:
- CPUs: 1
- Memory: 2048 MB
Synced Folders:
- Host directory . synced to /vagrant in the guest
- Host directory ./public synced to /usr/share/nginx in the guest

## Provisioning

The VM is provisioned using a shell script located at ./provision/base.sh. This script performs the following steps:

Update AlmaLinux:
- Installs the EPEL repository and updates the system packages.
Install NGINX Web Server:
- Installs NGINX and copies custom configuration files from the provision directory.
- Enables and starts the NGINX service.
Install MySQL Database Server:
- Installs MySQL server and enables it to start on boot.
- Configures the root user password and removes anonymous users and test databases for security.
Install PHP and Required Packages:
- Installs PHP and PHP-FPM along with necessary extensions (JSON, mbstring, MySQLnd, XML).
- Enables and starts the PHP-FPM service.
Cleanup:
- Cleans up package cache and removes unnecessary packages and log files.
- Notifies the user that provisioning was successful and provides the time taken for the process.

## Starting the VM

To start the Vagrant VM, run the following command:

```bash
vagrant up
```

This command will download the AlmaLinux 9 box (if not already downloaded), create the VM, and run the provisioning script.

## Accessing the Application

Once the VM is up and running, you can access your application by navigating to http://localhost:8080 in your web browser.

## SSH Access

To SSH into the VM, use the following command:

```bash
vagrant ssh
```

## Stopping the VM

To stop the VM, run:

```bash
vagrant halt
```

## Destroying the VM

If you want to remove the VM completely, use:

```bash
vagrant destroy
```

## Additional Notes

Ensure that your base.sh provisioning script is properly configured to install Nginx, MySQL/MariaDB, and PHP as needed for your LEMP stack.

Modify the Vagrantfile as necessary to suit your development needs.

## License

This project is licensed under the MIT License.
