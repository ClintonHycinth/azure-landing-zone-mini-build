# Azure Landing Zone Mini Build - Project Notes

## Step 1: Resource Group Creation

### Purpose

This step create the base structure for the Azure landing zone by setting up separate resource groups for shared services and workload resources.

### Implementation Steps

1. Signed in to the Azure Portal.
2. Search for **Resource groups** using the Azure search bar.
3. Open the **Resource groups** page.
4. Click **Create**.
5. Select the active subscription.
6. Enter the first resource group name as `rg-lz-shared-dev`.
7. Select `South Africa North` as the region.
8. Click **Review + create**.
9. Click **Create** to deploy the first resource group.
10. Repeated the same process to create the second resource group named `rg-lz-workload-dev`.
11. Confirm that both resource groups appeared in the Azure Portal after deployment.

### Configuration Used

- Resource Group 1: `rg-lz-shared-dev`
- Resource Group 2: `rg-lz-workload-dev`
- Region: `South Africa North`

### Why This Step Was Important

Creating the resource groups first helped organise the environment before deploying other resources. It also made it easier to separate shared services from workload resources.

### Result

Both resource groups were create successfully in Azure.

### Validation

The Azure Portal showed both resource groups:

- `rg-lz-shared-dev`
- `rg-lz-workload-dev`

This confirm that the initial environment structure was ready for the next stage of the project.

### Screenshot Evidence

- `screenshots/01-resource-groups.png`

## Step 2: Apply Tags to Resource Groups

### Purpose

This step added tags to the resource groups in order to improve organisation, ownership visibility, and project identification within the Azure environment.

### Implementation Steps

1. Open **Resource groups** in the Azure Portal.
2. Select the resource group `rg-lz-shared-dev`.
3. Open the **Tags** section from the resource group menu.
4. Added the following tags:
   - `Environment = Dev`
   - `Owner = Clinton`
   - `Project = LandingZoneMiniBuild`
   - `Purpose = Learning`
5. Click **Apply** to save the tags.
6. Repeated the same process for the second resource group `rg-lz-workload-dev`.
7. Confirm that both resource groups had the planned tags applied successfully.

### Configuration Used

Tags applied to both resource groups:

- `Environment = Dev`
- `Owner = Clinton`
- `Project = LandingZoneMiniBuild`
- `Purpose = Learning`

### Why This Step Was Important

Applying tags helps make Azure resources easier to organise and manage. It also supports governance by identifying the environment, project, ownership, and purpose of the resources.

### Result

The required tags were successfully applied to both resource groups.

### Validation

Both resource groups showed the expected tags in the Azure Portal:

- `Environment = Dev`
- `Owner = Clinton`
- `Project = LandingZoneMiniBuild`
- `Purpose = Learning`

This confirm that the resource groups were properly labelled for the project.

### Screenshot Evidence

- `screenshots/02-tags.png`

## Step 3: Create Log Analytics Workspace

### Purpose

This step create a Log Analytics Workspace to support monitoring and log collection for the Azure landing zone environment.

### Implementation Steps

1. Signed in to the Azure Portal.
2. Search for **Log Analytics workspaces** using the Azure search bar.
3. Open the **Log Analytics workspaces** page.
4. Click **Create**.
5. Select the active subscription.
6. Choose the resource group `rg-lz-shared-dev`.
7. Enter the workspace name as `log-lz-monitor`.
8. Select `South Africa North` as the region.
9. Click **Review + create**.
10. Click **Create** to deploy the workspace.
11. Confirm that the Log Analytics Workspace appeared successfully in Azure.

### Configuration Used

- Resource Group: `rg-lz-shared-dev`
- Workspace Name: `log-lz-monitor`
- Region: `South Africa North`

### Why This Step Was Important

The Log Analytics Workspace provides a central place for collecting and storing monitoring data. This supports visibility, troubleshooting, and alerting for resources deployed in the environment.

### Result

The Log Analytics Workspace was create successfully in Azure.

### Validation

The Azure Portal showed the workspace `log-lz-monitor` in the resource group `rg-lz-shared-dev`.

This confirm that the monitoring foundation for the project had been create successfully.

### Screenshot Evidence

- `screenshots/03-log-analytics-workspace.png`

## Step 4: Create Virtual Network and Subnets

### Purpose

This step create the main network structure for the Azure landing zone by deploying a virtual network and separating it into management and workload subnets.

### Implementation Steps

1. Signed in to the Azure Portal.
2. Search for **Virtual networks** using the Azure search bar.
3. Open the **Virtual networks** page.
4. Click **Create**.
5. Select the active subscription.
6. Choose the resource group `rg-lz-workload-dev`.
7. Enter the virtual network name as `vnet-lz-main-dev`.
8. Select `South Africa North` as the region.
9. Move to the **IP addresses** section.
10. Used the IPv4 address space `10.0.0.0/16`.
11. Create the first subnet named `snet-management` with the address range `10.0.1.0/24`.
12. Create the second subnet named `snet-workload` with the address range `10.0.2.0/24`.
13. Review the configuration.
14. Click **Create** to deploy the virtual network.
15. Confirm that the virtual network and both subnets appeared successfully in Azure.

### Configuration Used

- Resource Group: `rg-lz-workload-dev`
- Virtual Network Name: `vnet-lz-main-dev`
- Region: `South Africa North`
- Address Space: `10.0.0.0/16`
- Subnet 1: `snet-management` → `10.0.1.0/24`
- Subnet 2: `snet-workload` → `10.0.2.0/24`

### Why This Step Was Important

The virtual network provides the private network foundation for the landing zone. Creating separate subnets for management and workload purposes helps demonstrate basic network structure and logical separation within the Azure environment.

### Result

The virtual network and both planned subnets were create successfully in Azure.

### Validation

The Azure Portal showed the virtual network `vnet-lz-main-dev` with the address space `10.0.0.0/16` and the two configured subnets:

- `snet-management`
- `snet-workload`

This confirm that the network foundation for the project was ready for the next stage.

### Screenshot Evidence

- `screenshots/04-vnet-subnets.png`

## Step 5: Create Network Security Group and Associate It with the Workload Subnet

### Purpose

This step create a Network Security Group (NSG) and associated it with the workload subnet in order to introduce basic network traffic control into the Azure landing zone.

### Implementation Steps

1. Signed in to the Azure Portal.
2. Search for **Network security groups** using the Azure search bar.
3. Open the **Network security groups** page.
4. Click **Create**.
5. Select the active subscription.
6. Choose the resource group `rg-lz-workload-dev`.
7. Enter the NSG name as `nsg-lz-workload-dev`.
8. Select `South Africa North` as the region.
9. Click **Review + create**.
10. Click **Create** to deploy the Network Security Group.
11. Open the NSG after deployment.
12. Navigated to the **Subnets** section under Settings.
13. Click **Associate**.
14. Select the virtual network `vnet-lz-main-dev`.
15. Select the subnet `snet-workload`.
16. Saved the subnet association.
17. Confirm that the NSG was successfully linked to the workload subnet.

### Configuration Used

- Resource Group: `rg-lz-workload-dev`
- Network Security Group Name: `nsg-lz-workload-dev`
- Region: `South Africa North`
- Associated Virtual Network: `vnet-lz-main-dev`
- Associated Subnet: `snet-workload`

### Why This Step Was Important

The NSG provides a basic network security layer by controlling traffic at the subnet level. Associating it with the workload subnet helps demonstrate that the landing zone includes not only network structure but also security controls.

### Result

The Network Security Group was create successfully and associated with the workload subnet.

### Validation

The Azure Portal showed that `nsg-lz-workload-dev` was associated with the subnet `snet-workload` in the virtual network `vnet-lz-main-dev`.

This confirm that a basic network security control had been applied to the workload area of the environment.

### Screenshot Evidence

- `screenshots/05-nsg-subnet-association.png`

## Step 6: Implement Azure Policy for Tag Governance

### Purpose

This step applies Azure Policy assignments to introduce tag governance controls into the landing zone environment.

### Implementation Steps

1. Sign in to the **Azure Portal**.
2. Search for **Policy** using the Azure search bar.
3. Open the **Policy** service.
4. Navigate to the **Assignments** section.
5. Click **Assign policy**.
6. Select the scope as the **subscription**.
7. Choose the built-in policy definition **Require a tag on resource groups**.
8. Set the required tag name parameter to `environment`.
9. Review the assignment configuration.
10. Click **Review + create**.
11. Click **Create** to assign the policy.
12. Repeat the same process for the tag `project`.
13. Create another policy assignment using the built-in policy definition **Inherit a tag from the resource group if missing** for `environment`.
14. Enable **Create a remediation task** for the inherit-tag assignment.
15. Select **System assigned managed identity** for the modify-based policy assignment.
16. Review and create the assignment.
17. Repeat the same process for the tag `project`.
18. Create another policy assignment using the built-in policy definition **Require a tag on resources** for `environment`.
19. Review and create the assignment.
20. Repeat the same process for the tag `project`.
21. Confirm that all policy assignments appear successfully in Azure.

### Configuration Used

- Scope: `Subscription`
- Policy Definitions:
  - **Require a tag on resource groups**
  - **Inherit a tag from the resource group if missing**
  - **Require a tag on resources**
- Required Tag Names:
  - `environment`
  - `project`

### Why This Step Is Important

Azure Policy helps enforce rules and standards within an Azure environment. Using policy assignments to require tags on resource groups, inherit tags to resources, and require tags on resources demonstrates stronger governance and helps ensure consistency across deployed resources.

### Result

The policy assignments are created successfully at the subscription scope. Azure Policy also identifies existing resources that require remediation under the inherit-tag assignments.

### Validation

The Azure Portal shows the policy assignments under **Azure Policy Assignments** and lists remediation candidates under **Azure Policy Remediation**.

This confirms that tag governance controls are introduced across the landing zone environment.

### Screenshot Evidence

- `screenshots/06-policy-assignments.png`
- `screenshots/06-policy-remediation.png`

## Step 7: Review and Document the RBAC Access Model

### Purpose

This step reviewe the access control model for the landing zone environment in order to document how role-based access control (RBAC) supports secure and controlled administration.

### Implementation Steps

1. Signed in to the Azure Portal.
2. Search for **Resource groups** using the Azure search bar.
3. Open the resource group `rg-lz-workload-dev`.
4. Navigated to **Access control (IAM)**.
5. Reviewe the existing role assignments for the resource group.
6. Documented the intended RBAC model for the project.

### Configuration Used

The intended RBAC design for this project is:

- **Administrative role** for managing the environment
- **Read-only role** for viewing resources without making changes

Example role approach:

- `Contributor` for workload management
- `Reader` for visibility and review

Scope used for review:

- `rg-lz-workload-dev`

### Why This Step Was Important

RBAC is an important part of Azure governance because it controls who can access resources and what actions they can perform. Including an RBAC model in the project demonstrates awareness of least-privilege access and controlled administration.

### Result

The access control model for the workload resource group was reviewe and documented as part of the landing zone design.

### Validation

The Azure Portal showed the **Access control (IAM)** page for the resource group `rg-lz-workload-dev`, confirming that RBAC could be reviewed and managed at the resource group scope.

This supported the governance design of the landing zone project.

### Screenshot Evidence

- `screenshots/07-rbac-review.png`

## Step 8: Create and Configure the Linux Virtual Machine

### Purpose

This step deploys the sample workload for the Azure landing zone by creating a Linux virtual machine inside the workload subnet and applying additional post-deployment configuration.

### Implementation Steps

1. Sign in to the **Azure Portal**.
2. Search for **Virtual machines** using the Azure search bar.
3. Open the **Virtual machines** page.
4. Click **Create** and select **Azure virtual machine**.
5. Select the active subscription.
6. Choose the resource group `rg-lz-workload-dev`.
7. Enter the virtual machine name as `vm-lz-app-dev`.
8. Select `South Africa North` as the region.
9. Choose an Ubuntu Linux image for the virtual machine.
10. Select a small VM size supported by the subscription.
11. Configure the administrator account for the VM.
12. Allow inbound **SSH** access on port **22**.
13. Select the virtual network `vnet-lz-main-dev`.
14. Select the subnet `snet-workload`.
15. Add the required tags during the VM configuration.
16. Under **Boot diagnostics**, select **Enable with managed storage account (recommended)**.
17. Review the deployment configuration.
18. Click **Review + create**.
19. Click **Create** to deploy the virtual machine.
20. Confirm that the VM appears successfully in Azure after deployment.
21. Open the deployed virtual machine in the Azure Portal.
22. Under the **Operations** section, click **Auto-shutdown**.
23. Set **Auto-shutdown** to **On**.
24. Select the preferred shutdown time and time zone.
25. Enable notification by **email**.
26. Enter the email address to receive the auto-shutdown notification.
27. Click **Save** to apply the auto-shutdown configuration.

### Configuration Used

- Resource Group: `rg-lz-workload-dev`
- Virtual Machine Name: `vm-lz-app-dev`
- Region: `South Africa North`
- Image: `Ubuntu Server 22.04 LTS` or equivalent Ubuntu Linux image
- Network: `vnet-lz-main-dev`
- Subnet: `snet-workload`
- Inbound Port: `SSH (22)`
- Tags: `Required tags added`
- Boot Diagnostics: `Enable with managed storage account (recommended)`
- Auto-shutdown: `Configured after deployment`
- Auto-shutdown Notification: `Enabled by email`

### Why This Step Is Important

The Linux virtual machine serves as the sample workload for the landing zone. Deploying it inside the structured environment helps demonstrate that the landing zone is usable and ready to host resources. Applying boot diagnostics and auto-shutdown also improves visibility and cost control.

### Result

The Linux virtual machine is created successfully in Azure and deployed into the workload subnet. Boot diagnostics is enabled during deployment, and auto-shutdown is configured successfully after deployment with email notification enabled.

### Validation

The Azure Portal shows the virtual machine `vm-lz-app-dev` in the resource group `rg-lz-workload-dev`, connected to the virtual network `vnet-lz-main-dev` and subnet `snet-workload`.

The VM configuration also shows that boot diagnostics and auto-shutdown are enabled.

This confirms that the landing zone can host and manage a workload successfully.

### Screenshot Evidence

- `screenshots/08-linux-vm-overview.png`

## Step 9: Configure Recommended Alerts and Action Group for the Virtual Machine

### Purpose

This step configures recommended alert rules for the Linux virtual machine and creates an email-based action group to establish a basic monitoring and notification baseline for the landing zone environment.

### Implementation Steps

1. Sign in to the **Azure Portal**.
2. Search for **Virtual machines** using the Azure search bar.
3. Open the virtual machine `vm-lz-app-dev`.
4. Navigate to the **Alerts** section for the virtual machine.
5. Open the **Recommended alert rules** configuration page.
6. Review the available recommended alert rules for the virtual machine.
7. Enable the alert rule **Percentage CPU** with the threshold set to **greater than 80**.
8. Enable the alert rule **Available Memory Bytes** with the threshold set to **less than 1**.
9. Enable the alert rule **VmAvailabilityMetric** with the threshold set to **less than 1**.
10. Leave the following alert rules disabled:
    - **Data Disk IOPS Consumed Percentage** greater than **95**
    - **OS Disk IOPS Consumed Percentage** greater than **95**
    - **Network In Total** greater than **500**
    - **Network Out Total** greater than **200**
11. Enable **Email** notification.
12. Enter the notification email address as `hycinthclinton995@gmail.com`.
13. Review the estimated monthly cost shown for the selected alert configuration.
14. Click **Save** to create the recommended alert rules and the associated action group.

### Configuration Used

- Virtual Machine: `vm-lz-app-dev`
- Alert Rules Enabled:
  - `Percentage CPU > 80`
  - `Available Memory Bytes < 1`
  - `VmAvailabilityMetric < 1`
- Alert Rules Disabled:
  - `Data Disk IOPS Consumed Percentage > 95`
  - `OS Disk IOPS Consumed Percentage > 95`
  - `Network In Total > 500`
  - `Network Out Total > 200`
- Notification Method: `Email`
- Notification Email: `put your notification email`
- Action Group: `Created and linked to the alert rules`
- Estimated Monthly Total: `0.30 USD`

### Why This Step Is Important

Recommended alert rules help introduce a basic operational monitoring layer for the virtual machine. Creating an action group alongside the alert rules ensures that notifications are sent when selected alert conditions are met, improving visibility into VM health and availability.

### Result

The recommended alert rules are created successfully for the virtual machine, and an email-based action group is created and linked to the alert rules for notification delivery.

### Validation

The Azure Portal shows the configured alert rules under the virtual machine alert configuration and shows the associated action group under the notification settings.

This confirms that the virtual machine now has a basic alerting and notification baseline in place.

### Screenshot Evidence

- `screenshots/09-vm-recommended-alerts.png`

## Step 10: Enable Monitoring for the Virtual Machine

### Purpose

This step enables enhanced monitoring for the Linux virtual machine to collect guest-level performance and health data for improved visibility and troubleshooting.

### Implementation Steps

1. Sign in to the **Azure Portal**.
2. Search for **Virtual machines** using the Azure search bar.
3. Open the virtual machine `vm-lz-app-dev`.
4. Navigate to the **Monitor** section for the virtual machine.
5. Click **Configure** to enable enhanced monitoring.
6. Open the monitoring configuration page.
7. Leave **[Classic] Log-based metrics** enabled.
8. Select the existing **Log Analytics workspace** `log-lz-monitor`.
9. Disable **[Preview] OpenTelemetry metrics** and do not use the default Azure Monitor workspace option.
10. Review the monitoring configuration.
11. Click **Review + enable**.
12. Click **Enable** to apply the monitoring configuration.
13. Confirm that the monitoring setup completes successfully.

### Configuration Used

- Virtual Machine: `vm-lz-app-dev`
- Monitoring Type: `Logs-based (classic)`
- Log Analytics Workspace: `log-lz-monitor`
- OpenTelemetry Metrics: `Disabled`
- Azure Monitor Workspace: `Not used`

### Why This Step Is Important

Enhanced monitoring provides deeper visibility into the virtual machine by collecting guest-level performance and health data. Using the logs-based monitoring experience with an existing Log Analytics workspace allows monitoring to be enabled without relying on Azure to create new default monitoring resource groups.

### Result

Enhanced monitoring is enabled successfully for the virtual machine using the logs-based monitoring experience and the existing Log Analytics workspace `log-lz-monitor`.

### Validation

The Azure Portal shows that monitoring is enabled for the virtual machine and that the configuration uses the existing Log Analytics workspace.

This confirms that the virtual machine is onboarded for enhanced monitoring using the logs-based monitoring path.

### Screenshot Evidence

- `screenshots/10-vm-monitoring-config.png`

## Step 11: Final Validation of the Landing Zone Environment

### Purpose

This step validates the key components of the Azure landing zone to confirm that the environment is built successfully and that the main governance, networking, monitoring, alerting, and workload elements are in place.

### Implementation Steps

1. Open **Resource groups** in the Azure Portal and confirm the existence of `rg-lz-shared-dev` and `rg-lz-workload-dev`.
2. Review the tags on both resource groups and confirm that the required tags are applied.
3. Open the **Log Analytics workspace** `log-lz-monitor` and confirm that it exists in `rg-lz-shared-dev`.
4. Open the virtual network `vnet-lz-main-dev` and confirm the address space and subnet configuration.
5. Open the Network Security Group `nsg-lz-workload-dev` and confirm its association with the workload subnet.
6. Open **Azure Policy** and confirm that the tag governance assignments for `environment` and `project` exist at the **subscription** scope.
7. Open the Linux virtual machine `vm-lz-app-dev` and confirm that it exists in `rg-lz-workload-dev` and is connected to the expected virtual network and subnet.
8. Review the VM configuration and confirm that **Boot diagnostics** is enabled and **Auto-shutdown** is configured.
9. Open the VM **Insights** page and confirm that log-based monitoring is enabled using the Log Analytics workspace `log-lz-monitor`.
10. Open the VM **Alerts** configuration and confirm that the recommended alert rules are in place.
11. Confirm that the alert notification action group is configured with email notification.

### Configuration Validated

- Resource Groups:
  - `rg-lz-shared-dev`
  - `rg-lz-workload-dev`
- Log Analytics Workspace:
  - `log-lz-monitor`
- Virtual Network:
  - `vnet-lz-main-dev`
- Subnets:
  - `snet-management`
  - `snet-workload`
- Network Security Group:
  - `nsg-lz-workload-dev`
- Policy Scope:
  - `Subscription`
- Required Policy Tags:
  - `environment`
  - `project`
- Virtual Machine:
  - `vm-lz-app-dev`
- Monitoring Type:
  - `Log-based (Classic)`
- Alerting:
  - Recommended alert rules enabled
  - Email-based action group configured

### Why This Step Is Important

Final validation helps confirm that the landing zone is not only deployed but also structured and operating as intended. It verifies that the environment includes governance, network organisation, monitoring, alerting, and a working workload.

### Result

The main components of the landing zone are present and configured as planned.

### Validation

The Azure Portal shows that the shared and workload resource groups, monitoring workspace, network components, policy assignments, Linux virtual machine, monitoring configuration, recommended alert rules, and action group are all deployed and available.

This confirms that the Azure landing zone mini build is completed successfully.

### Screenshot Evidence

- `screenshots/11-final-validation.png`

## Step 12: Prepare and Push the Project to GitHub

### Purpose

This step prepares the completed Azure landing zone project for publication on GitHub so it can be used as public portfolio evidence.

### Implementation Steps

1. Review the local project folder to confirm that the `README.md` file, screenshots, and supporting notes are present.
2. Create a new public GitHub repository named `azure-landing-zone-mini-build`.
3. Open the project folder in **Visual Studio Code**.
4. Open the integrated terminal in **VS Code**.
5. Run `git init` to initialize the local Git repository.
6. Run `git add .` to stage all project files.
7. Run `git commit -m "Initial commit - Azure landing zone mini build"` to create the first commit.
8. Run `git branch -M main` to rename the default branch to `main`.
9. Run `git remote add origin https://github.com/ClintonHycinth/azure-landing-zone-mini-build.git` to connect the local project folder to the GitHub repository.
10. Run `git push -u origin main` to push the project to GitHub.
11. Confirm that the project files appear successfully in the GitHub repository.

### Configuration Used

- Repository Name: `azure-landing-zone-mini-build`
- Repository Visibility: `Public`
- GitHub Username: `ClintonHycinth`
- Default Branch: `main`

### Why This Step Is Important

Publishing the project to GitHub makes it easier to reference in a resume, LinkedIn profile, and interviews. It also provides visible proof of hands-on Azure project work.

### Result

The Azure landing zone mini build project is published successfully to GitHub.

### Validation

The GitHub repository shows the `README.md` file, screenshots, and supporting project files after the push completes successfully.

This confirms that the project is ready to be shared publicly as part of a cloud engineering portfolio.
