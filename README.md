# HDInsightTutorial Using Azure PowerShell

##1. Creating HDInsight cluster using Powershell

## Prerequisites:
* Azure subscription or free trial account
	* [30 day free trial](https://azure.microsoft.com/en-us/resources/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)
  * [Install PowerShell](https://docs.microsoft.com/en-us/powershell/azureps-cmdlets-docs/)
    If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.
    * Step 1. Make sure run Windows PowerShell as an administrator. Install the latest Azure PowerShell from the PowerShell Gallery using an elevated Windows PowerShell or PowerShell Integrated Scripting Environment (ISE) prompt:
     ```
     Install-Module AzureRM
     ```
    
    * Step 2.
    
  To check the version of the installed PowerShell:
  ```
  Get-Module *azure*
  ```
 * To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:+
    * Create an Azure resource group
    * Create an Azure Storage account
    * Create an Azure Blob container
    * Create an HDInsight cluster