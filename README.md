# GetDLPInformation
This PS script gives the information about the Power Apps DLP policy in Power plat form environment. Before running this PS script you need to have Powershell modules for Powerplatform installed. Morei information can be found at https://docs.microsoft.com/en-us/power-platform/admin/powerapps-powershell#data-loss-prevention-dlp-policy-commands

Below is the comple PS Script

$currentTime = $(Get-Date).ToString("yyyymmddhhmmss");
#Make sure to update the path to your needs
$outputFile="C:\Output\ConnectorsInfo-"+$currentTime+".csv";
Add-Content -Path $outputFile -Value "Connector ID,Connector Name,Connector Type";
Add-PowerAppsAccount
#The below command is getting for business data group. For non business category, simpy replace 'BusinessDataGroup' with 'NonBusinessDataGroup'
$businessCategoryConnectors = Get-AdminDlpPolicy '(Default) Policy 08:29:45 01-14-2017' | Select –ExpandProperty BusinessDataGroup
foreach($connector in $businessCategoryConnectors)
{
    $connectorID = $connector.id;
    $connectorName = $connector.name;
    $connectorType = $connector.type;
    Add-Content -Path $outputFile -Value "$connectorID,$connectorName,$connectorType";
}
