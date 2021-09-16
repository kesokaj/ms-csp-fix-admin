````
### VARIABLES
$partnerTenant = Read-Host "Enter Partner tenant name ex Dist or reseller"
$customerTenant = Read-Host "Enter customer tenant id"
$subscription = Read-Host "Enter subscriptionid where admin agent is missing"
### END VARIABLES

#1 Authenticate to partner tenant
Connect-AzAccount -Tenant $partnerTenant
Get-AzADGroup -DisplayName AdminAgents

#2 Copy data
Read-Host "Copy information. Then press any key to continiue"

#3 Fix modules
Update-Module Az.Resources

#4 Connect to Customer tenant(reseller or end customer)
Connect-AzAccount -TenantID $customerTenant

#5 Set context
Set-AzContext -SubscriptionID $subscription

#6 Reset rights
New-AzRoleAssignment -ObjectID $($copiedData = Read-host "Enter copied data") -RoleDefinitionName "Owner" -Scope "/subscriptions/'$subscription'"






#### EXTRA
Install-Module -Name Az.Resources -Force -Verbose
Import-Module -Name Az.Resources -Verbose -MinimumVersion 4.1.1
Connect-AzAccount -Tenant $customerTenant
Set-AzContext -SubscriptionId $subscription
New-AzRoleAssignment -ObjectId $($copiedData = Read-host "Enter copied data") -RoleDefinitionName "Owner" -Scope "/subscriptions/$subscription" -ObjectType "ForeignGroup"

````
