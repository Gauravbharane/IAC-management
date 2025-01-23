# IAC-management

Full blog link - https://gauravbharane.medium.com/manage-cloud-servers-using-iac-c9a5d8dec1af.
<hr>
View my Presentation - https://www.canva.com/design/DAFutgOgQrQ/Qw_MkRGVfq1iOkkzLlo-Iw/view?utm_content=DAFutgOgQrQ&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink
<hr>

![My Project Screenshot](https://github.com/gauravbharane/IAC-management/raw/main/Infrastruture_as_code_project.png)

In today’s fast-paced technological landscape, managing infrastructure efficiently is crucial for any organization. Infrastructure as Code (IaC) has revolutionized the way we deploy, manage, and scale our infrastructure. In this blog post, I’ll share my experience of creating and managing Linux servers on Akamai Cloud (Linode) using IaC tools like Terraform and Ansible. This project aimed to achieve a scalable, automated, and efficient infrastructure setup.

Why Akamai Cloud (Linode)?

Akamai Cloud (Linode) is renowned for its simplicity, powerful infrastructure, and cost-effective solutions. It offers a range of services that are ideal for developers and businesses looking to deploy and manage their applications in the cloud. With a straightforward interface and robust API, Linode provides the perfect platform for leveraging IaC tools like Terraform and Ansible.

Getting Started with Terraform

Terraform is an open-source IaC tool that allows you to define and provision your infrastructure using a declarative configuration language. It enables you to manage your infrastructure as code, making it easier to version control, share, and reuse.

Step 1: Install Terraform

To get started, download and install Terraform from the official website. Verify the installation by running:

# For Centos/RHEL systems
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install terraform
Step 2: Configure Terraform for Linode

Create a directory for your Terraform configuration files and navigate to it:

mkdir linode-terraform
cd linode-terraform
Create a main.tf file and configure the Linode provider and resources:

# main.tf
provider "linode" {
  token = "<YOUR_LINODE_API_TOKEN>"
}
resource "linode_instance" "example" {
  label        = "terraform-example"
  region       = "us-west"
  image        = "linode/ubuntu20.04"
  root_pass    = "yourpassword"
  type         = "g6-nanode-1"
}
output "linode_ip" {
  value = linode_instance.example.ip_address
}
Initialize and apply the configuration:

terraform init
terraform apply
Automating Configuration with Ansible

Ansible is a powerful configuration management tool that automates the provisioning, configuration, and management of servers. It uses simple, human-readable YAML files to define automation tasks.

Step 1: Install Ansible

Install Ansible using the appropriate package manager for your system:

# For Centos/RHEL systems
sudo dnf install ansible
Verify the installation:

ansible --version
Step 2: Create Ansible Playbook

Create a directory for your Ansible files and navigate to it:

mkdir ansible-playbook
cd ansible-playbook
Create an inventory file listing your Linode server:

vim inventory
# inventory

[Groupname]
<LINODE_SERVER_IP>
Create a playbook file to automate server setup and configuration:

vim playbook.yml
# playbook.yml
- name: Configure Linode Server
  hosts: linodes
  become: yes
  tasks:
    - name: Update and upgrade apt packages
      apt:
        update_cache: yes
        upgrade: dist
        cache_valid_time: 3600
   - name: Install necessary packages
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - nginx
        - git
Step 3: Run Ansible Playbook

Execute the playbook using the following command:

ansible-playbook -i inventory playbook.yml
Monitoring and Optimization

Effective monitoring is essential for maintaining the health and performance of your infrastructure. Linode provides Longview, a powerful monitoring tool that offers real-time insights into your server’s performance. Additionally, custom scripts and third-party monitoring solutions can be integrated to provide comprehensive monitoring.

Optimization Tips

Resource Utilization: Regularly review and optimize server configurations to ensure efficient resource utilization.
Cost Management: Implement cost-saving measures such as using smaller instance types during off-peak hours.
Scalability: Use Terraform to automate scaling operations, ensuring your infrastructure can handle varying workloads.
Conclusion

Managing Linux servers on Akamai Cloud (Linode) using Terraform and Ansible provides a powerful combination of automation, scalability, and efficiency. By leveraging IaC tools, you can achieve a robust and reliable infrastructure setup, freeing up time to focus on innovation and development.

I hope this blog post has provided you with valuable insights into using Terraform and Ansible to manage your cloud infrastructure. Feel free to reach out with any questions or share your experiences in the comments below.

Happy coding!
