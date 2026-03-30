# Windows-Patching-Project

# Project Synopsis: Automated Azure Windows Patching via Ansible

Project Overview
This project provides a custom automation framework to handle Windows Patching across an Azure-hosted infrastructure. By combining Ansible orchestration with specialized PowerShell deployment scripts, we have moved from a manual patching process to a scheduled, touchless automation model.

⚙️ Execution Workflow
Preparation: KB articles are downloaded and converted into executable .bat files for deployment.
Custom Deployment: A specialized PowerShell script manages the transfer and installation of these patch files onto the target Windows servers.
Targeting (Manual Limit): To ensure precision, target hosts are manually specified using the Limit field within the Ansible Job Template.
Scheduling: Patching jobs are scheduled in Ansible to align with approved Change Windows.
Execution & Reboot: Once triggered, the playbook executes the installation and performs a controlled system reboot to finalize the updates.
Compliance Reporting: Post-patching results and logs are automatically saved to a centralized SFS (Shared File System) link. This provides the Compliance Team with real-time visibility into the patching status and success rates.

🛠 Prerequisites
Connectivity: Ansible must reach target VMs via WinRM (Port 5986) with SSL/SChannel enabled.
Azure Fabric: Outbound access to 168.63.129.16 (Ports 80/32526) must be open for VM health monitoring.
Permissions: The Ansible Service Account requires administrative rights on the target servers to execute the PowerShell installer and trigger reboots.

"Next Steps":
SFS Mapping: Make sure your PowerShell script includes a command to map the SFS drive 
(e.g., New-PSDrive) so it can save the output log even after a reboot.
Error Handling: Since you are using a .bat file, ensure your script checks the Exit Code (usually 0 or 3010 for success/reboot required) so Ansible knows if the task truly passed.
