# ERPNext-Version14---Installation + Healthcare Module..
### ERPNext Version14 - Installation through the Virtual Box


# ERPNext Version14 Installation Guide with Healthcare Module:

## Prerequisites:
1. VirtualBox.
2. ERPNext Version14 .OVA file available in the Frappe Forum:
   https://mega.nz/file/LMdyQS6Z#R9ZxJTC0meQr63BD9Oi7K4e9Dz02S7-Z_LHmpkh0Bko

## Import and Start ERPNext Instance:
   Step 1: Import the downloaded ERPNext version 14 file in Virtual Box.
   
   Step 2: After Import, Click Start button in Virtual Box.
   
   Step 3: After clicking the Start button it will takes some times to run the Instance.

## SSH Installation (Default password: frappe):
   1. `sudo apt update`
   2. `sudo apt install openssh-server`
   3. `sudo systemctl status ssh`
   4. `sudo systemctl enable --now ssh`
   5. `ssh localhost`
   6. `sudo gedit /etc/ssh/sshd_config`
   7. `sudo systemctl restart ssh`
   8. `sudo systemctl status ssh`
   9. `sudo localhost -p 2244…`

## Enable SSH:
   1. `sudo rm -f /etc/ssh/sshd_not_to_be_run`
   2. `sudo systemctl enable ssh`
   3. `sudo systemctl start ssh`

## Installation of Healthcare Module in ERPNext Version 14 (Two Methods):
  ### Method 1:
   1. Navigate to the directory (frappe-bench): `cd frappe-bench`
   2. `bench get-app Healthcare`
   3. `bench --site frappe.com install-app healthcare`
   4. `bench --site frappe.com migrate`
   5. `sudo reboot`

  ### Method 2:
    1. Navigate to the directory (frappe-bench): `cd frappe-bench`
    2. `bench get-app --branch version-14 https://github.com/frappe/healthcare`
    3. `bench --site frappe.com install-app healthcare`
    4. `bench --site frappe.com migrate`
    5. `bench --site frappe.com clear-cache`
    6. `bench --site frappe.com build`
    7. `sudo supervisorctl restart all`
    8. `sudo reboot`

## Restore Backup in ERPNext Version 14:
   Step 1: Download the latest backup file in the ERPNext Web Instance. (Screen Name: Download Backup).
   
   Step 2: After downloading the latest backup file, now you can restore it into the latest version of ERPNext Version14.
   
   Step 3: Now you can copy or move the unzip backup file in the windows local to ubuntu server using this cmd, In cmd prompt goto the backuo file downloaded directory then, use this cmd to move the Local 
           file into the Ubuntu Server--> scp name_of_the_backup_file.sql.gz username@ip_address:/home/to/frappe (which directory you want to move).
           For Ex -- scp 20231204_060002-ahp_medicall_in-database.sql.gz frappe@192.168.29.107:/home/frappe/frappe-bench 
           
## Below Steps to follow the Restore process:
   Step 1: ls (to list the sites in the frappe-bench directory)
   
   Step 2: gunzip name_of_the_backup_file.sql.gz
    	      (For ex: gunzip ahp.sql.gz)
           
   Step 3: ls
   
   Step 4: bench –site sitename –force restore name_of_the_backup_file.sql
    	      (For ex: bench –site frappe.com –force restore ahp.sql)
           
   Step 5: sudo reboot...
