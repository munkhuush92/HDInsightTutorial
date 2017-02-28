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
     
     ![To install and replace over the old version, please enter "A"](/images/install.png)
     
    Then, if it is successfully started, it should show this progress:
    
    ![progress](/images/progress.png)
    * Step 2. Connect to an Azure account
    	* To login Azure account from Azure Shell, type in the shell: 
	
		```
		Login-AzureRmAccount
		```
		* After that, it will pop up the browser for you to enter your credentials
			![loginpopup](/images/loggingin.png)
		* If logged successfully, then it will show your info
			![loginsuccess](/images/loginsucess.png)
		
    

 ##2. To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:
    * Create an Azure resource group:+
    	* Step 1. Create a variable for group name
	
		```
		$resGroupName = "yourdesiredgroupname"
		```
    * Create an Azure Storage account
    * Create an Azure Blob container
    * Create an HDInsight cluster
	
