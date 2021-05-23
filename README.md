<p>The files in this repository were used to configure the network depicted below.</p>
<p><a href="https://github.com/felixwubootcamp/Homework_13-Github/blob/main/Homework_12_-Cloud-Security.png" target="_blank" rel="noopener noreferrer"><img src="https://github.com/felixwubootcamp/Homework_13-Github/blob/main/Homework_12_-Cloud-Security.png" alt="Diagram" /></a></p>
<p>These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.</p>
<p><a href="https://github.com/felixwubootcamp/Homework_13-Github/blob/main/Ansible/filebeat-playbook%2Byml.txt">filebeat-playbook.yml</a></p>
<p>More Install and playbook files can be found on <a href="https://github.com/felixwubootcamp/Homework_13-Github/tree/main/Ansible">here</a></p>
<p>This document contains the following details:</p>
<ul>
<li>Description of the Topologu</li>
<li>Access Policies</li>
<li>ELK Configuration
<ul>
<li>Beats in Use</li>
<li>Machines Being Monitored</li>
</ul>
</li>
<li>How to Use the Ansible Build</li>
</ul>
<h3>Description of the Topology</h3>
<p>The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.</p>
<p>Load balancing ensures that the application will be highly available for customers, in addition to restricting attacks to the network. If a server goes down, or needs to be updated, services will still continue. -The advantage of using a jump box is that only the jump box can access the Virutal network via ssh.</p>
<p>Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.</p>
<ul>
<li>Filebeat monitors the log files or locations specified, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.</li>
<li>Metricbeat is an extremely easy-to-use, efficient and reliable metric shipper for monitoring your system and the processes running on it. The configuration details of each machine may be found below.</li>
</ul>
<table style="height: 90px;">
<thead>
<tr style="height: 18px;">
<th style="height: 18px; width: 79px;">Name</th>
<th style="height: 18px; width: 75px;">Function</th>
<th style="height: 18px; width: 290px;">IP Address</th>
<th style="height: 18px; width: 141px;">Operating System</th>
</tr>
</thead>
<tbody>
<tr style="height: 18px;">
<td style="height: 18px; width: 79px;">Jump-Box</td>
<td style="height: 18px; width: 75px;">Gateway</td>
<td style="height: 18px; width: 290px;">Public: 40.86.160.61 Private: 10.0.0.150</td>
<td style="height: 18px; width: 141px;">ubuntu</td>
</tr>
<tr style="height: 18px;">
<td style="height: 18px; width: 79px;">Web-1</td>
<td style="height: 18px; width: 75px;">Server</td>
<td style="height: 18px; width: 290px;">Public: 40.86.164.99 Private: 10.0.0.160</td>
<td style="height: 18px; width: 141px;">ubuntu</td>
</tr>
<tr style="height: 18px;">
<td style="height: 18px; width: 79px;">Web-2</td>
<td style="height: 18px; width: 75px;">Server</td>
<td style="height: 18px; width: 290px;">Public: 40.86.164.99 Private:10.0.0.170</td>
<td style="height: 18px; width: 141px;">ubuntu</td>
</tr>
<tr style="height: 18px;">
<td style="height: 18px; width: 79px;">ELK-Server</td>
<td style="height: 18px; width: 75px;">Monitoring</td>
<td style="height: 18px; width: 290px;">Public: 52.233.79.129 Private: 10.2.0.4</td>
<td style="height: 18px; width: 141px;">ubuntu</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>Access Policies</p>
<p>The machines on the internal network are not exposed to the public Internet.</p>
<p>Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:</p>
<ul>
<li>Add whitelisted IP addresses:- - Public IP address which changes sometime when the VM is on/off eg of Public IP <strong>your work public IP Address</strong></li>
</ul>
<p>Machines within the network can only be accessed by SSH.</p>
<ul>
<li>Which machine did you allow to access your ELK VM? What was its IP address?</li>
<li>JumpBox VM, its private Ip address(Vnet IP)-10.1.150</li>
</ul>
<p>A summary of the access policies in place can be found in the table below.</p>
<table style="width: 402px; height: 108px;">
<thead>
<tr style="height: 36px;">
<th style="width: 69px; height: 36px;">Name</th>
<th style="width: 145px; height: 36px;">Publicly Accessible</th>
<th style="width: 166px; height: 36px;">Allowed IP Addresses</th>
</tr>
</thead>
<tbody>
<tr style="height: 18px;">
<td style="width: 69px; height: 18px;">Jump Box</td>
<td style="width: 145px; height: 18px;">yYES</td>
<td style="width: 166px; height: 18px;">10.1.0.150</td>
</tr>
<tr style="height: 18px;">
<td style="width: 69px; height: 18px;">Web-1</td>
<td style="width: 145px; height: 18px;">NO</td>
<td style="width: 166px; height: 18px;">10.1.0.150</td>
</tr>
<tr style="height: 18px;">
<td style="width: 69px; height: 18px;">Web-2</td>
<td style="width: 145px; height: 18px;">NO</td>
<td style="width: 166px; height: 18px;">10.1.0.150</td>
</tr>
<tr style="height: 18px;">
<td style="width: 69px; height: 18px;">Elk-VM1</td>
<td style="width: 145px; height: 18px;">NO</td>
<td style="width: 166px; height: 18px;">10.1.0.150</td>
</tr>
</tbody>
</table>
<h3>Elk Configuration</h3>
<p>*Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...</p>
<ul>
<li>
<p>What is the main advantage of automating configuration with Ansible?</p>
<ul>
<li>One main advantage would be YAML Playbooks. It is the best alternative for configuration management/automation.</li>
<li>It is also able to automate complex multi-tier IT application environemtns.</li>
</ul>
</li>
</ul>
<p>*The playbook implements the following tasks:</p>
<ul>
<li>
<p>In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._</p>
<ul>
<li>First I, SSH into the Jump-Box-Provisioner (ssh sysadmin@40.86.160.61)</li>
<li>Start/Attached to the ansible docker (sudo container list -a) (sudo docker start cranky_brown)/(sudo docker attach cranky_brown)</li>
<li>Went to /etc/ansible/roles directory and created the ELK playbook (install-ELK_Playbook.yml)</li>
<li>Ran the Elk_Playbook.yml in that same directory (install-Elk_Playbook.yml)</li>
<li>Lastly, I SSH into the ELK-VM to verify the server is up and running.</li>
</ul>
</li>
</ul>
<p>*The <a href="https://github.com/felixwubootcamp/Homework_13-Github/blob/main/Screenshot%202021-05-23%20133737.png" target="_blank" rel="nofollow">following screenshot</a> displays the result of running&nbsp;<code>docker ps</code>&nbsp;after successfully configuring the ELK instance.</p>
<p>&nbsp;</p>
