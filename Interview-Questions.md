Interview Questions

Domain: Network Security
**Faulty Firewall**
There is a firewall that was supposed to block SSH connections into a network, but instead lets them through. How would I troubleshoot this?


In the projects that i did for VMs, the security rule that was added on the network security group was to allow SSH connections only to the 
public ip address from my workstation to the Jumpbox VM and to block all other traffic into the Vnet.
If i try to connect to the ELK VM or to any the other two VMs in the 2 Vnets over SSH from my workstation (public ip), the connection will fail. The Jumpbox was the only VM that was configured to access all the VMs over SSH. The firewall rule that was added was to allow only the Jumpbox VM to access all the VMs in the virtual networks over SSH. All incoming traffic using SSH will need to go through the Jumpbox. The jump box sits in front of other machines that are not exposed to the public internet.


If one of my Project 1 VMs accepted SSH connections, i will verify if the Jumpbox VM is stopped or running in the VM panel. Restart the VM. Then i will verify the firewall rule for the Jumpbox in the network security group. Confirmed that only my public ip is allowed and others blocked. Confirmed that my ip is the same as in the rule. Verify the SSH port that Jumpbox is running on with ssh_config on the Jumpbox : sudo grep Port /etc/ssh/sshd_config. It should be port 22. Destination ip should be the private ip of the Jumpbox. Re-added the rule. Confirmed that  everything have been re-added; re-started and running (verify if ssh running :sudo systemctl status ssh). I will try to connect to the Jumpbox and try to connect to one of the VM over SSH to test the configuration.

 Project 1 network is not "immune" to cyber attacks. By installing a Jumpbox as a primary node and adding firewall rules to restrict traffic to the network will make it harder for attackers to penetrate the network.

 I can make the use of any monitoring authentication logs such as Datalog; ELK stack to monitor, visualize, log data to identify any suspicious authentication attempts.


 Domain: Cloud Security
 **Containers**
 When is it appropriate to use containers in cloud deployments, and what are the security benefits of doing so?

In project 1, I installed a Docker container that runs Ansible on the Jumpbox to configure other servers.  Ansible container was also used to connect to another VM and make configuration changes. Ansible files (ansible.cfg, hosts) had to be modified with ip addresses and login information to be able to connect to different VMs. I created Ansible playbooks (YAML file) to change specific configurations and to install applications on the VMs (ELK and DVWA on the web VMs).

Container was used in this project because of the following : It requires less system resources and don't include operating system images. Applications running in containers can be deployed easily to multiple different operating systems and hardware platforms. It consists of an entire runtime environment: an application, plus all its dependencies, libraries and other binaries, and configuration files needed to run it, bundled into one package. It runs a single operating system, and each container shares the operating system kernel with the other containers. They are much more lightweight and use far fewer resources. Size of container smaller(MB) than VM(GB). Containerized applications can be started almost instantly. The setup is quick and easy to use. Security benefits: isolating applications from the host system and from each other. Security measures and policies which includes container images, containers, the hosts, registries, runtimes.

In Project 1, I used the Ansible playbooks to configure the docker container to run on the VMs. Each playbook template has different sections to configure the settings that are needed for the downloads, the image, the module to install, enable the service, launch a specific container and any other settings. After the containers have been downloaded, i listed the containers docker container list -a. Check the status of that container sudo docker ps -a. I started the container, sudo docker start container_name then i attached the container sudo docker attach container_name. When i was in the container, i was able to connect to the 2 web servers and the ELK server over SSH. I was also able to get to DVWA Web servers (web-1, web-2) and Kibana (ELK server) on the web.

It would be possible to achieve the same set up in project 1 by using Virtual Machines or a local machine. Since VMs have their own OS, they can be fully isolated and thus more secure. On the other hand, VMs are large and take a long time to download and deploy. If you clone an entire VM, most of the VM will be wasted space. Containers are much more lightweight. When using conatiners, there will be a massive cost and operational savings by eliminating a large amount of file and CPU overhead. They can be recreated very easily.