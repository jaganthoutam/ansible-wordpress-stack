# ansible-wordpress-stack
This repo installs wordpress on an Amazon Web Services instance using an ansible playbook. Although the instructions here are for AWS, they should work equally well on other kinds of remote computers, provided they have the yum package manager installed.  

The playbook is organized into these roles:
* mysql     - mysql database
* php-fpm   - php support
* nginx     - web server
* wordpress - wordpress app

Each of these roles has its own subdirectory structure containing tasks and supporting files.

## Prerequisites
1. A local unix, linux, or mac OSX computer that has Ansible and git installed.
2. A running AWS instance with Amazon linux, a public IP address,  and an SSH key pair.
3. A file copy of the private SSH key on your local computer.
4. A domain name that maps to the public IP address of the AWS instance (optional - you can use the public IP in place of a domain name)

## Installing Wordpress
1. Clone this repo to your local computer

        git clone http://github.com/tomlamphier/ansible-wordpress-stack.git
2. Copy the SSH private key to the project directory.
3. Edit the hosts file; replace the IP address there with the public IP (or a domain name) for the AWS instance; set ansible_ssh_private_key_file variable to point to your private key.
4. Update the connect script to point to the private SSH key and the AWS instance. Run the script as a quick test of your connectivity to the AWS instance:

        ./connect
You should get an auth message on the first pass-simply say 'yes'.  If you see the AWS Amazon Linux welcome message, you are OK. Use logout to exit.

5. Edit the group_vars/all config file, set a password for the mysql root user (mysql_root_password) and wordpress (wp_db_password).
6. Run playbook:

        ansible-playbook -i hosts playbook.yml
7. Bring up a web browser and go to the domain name (or IP) of your instance.  You should see a wordpress page.  Provide the requested info about your blog.  Once this is done, your site is up.  Save your wordpress ID and password.
8. To customize the blog or add content, go to
       your-domain/wp-admin
       your-ip/wp-admin

## Reference
An blog post to bring you up to speed on Ansible: [Ansible Quick Start](http://datasciex.com/?p=230)

