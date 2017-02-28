# HDInsightTutorial Using Azure PowerShell
https://github.com/munkhuush92/HDInsightTutorial
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
    * Create an Azure resource group:
    	* Step 1. Create a variable for group name. 
	
		```
		$resGroupName = "yourdesiredgroupname"
		```
		
		* Step 2. Using groupname variable to create resource group. Location can be anywhere.

			```
			New-AzureRmResourceGroup -Name $resGroupName -Location "South Central US"
			```
			If created successfully, then it should show the result

			![resourcegroupsuccess](/images/resgroupnamesuccess.png)
			
		* I created a multiple of variable so that I can use it later process. (Short Cut)
		
		Make sure $token is all in lowercase because we will use it for storage name and storage name must be all lower-case
			![resourcegroupsuccess2](/images/rescreated.png)
		
			
    * Create an Azure Storage account
    
    	Type the following in PowerShell to create a storage
		
		```
		# Create an Azure Storage account and container used as the default storage
		New-AzureRmStorageAccount `
    		-ResourceGroupName $resourceGroupName `
    		-StorageAccountName $defaultStorageAccountName `
   		-Location $location `
    		-Type Standard_LRS
		$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -Name $defaultStorageAccountName -ResourceGroupName $resourceGroupName)[0].Value
		$destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
		```
		
	If created successfully, it should display below
	
	 ![storagesuccess](/images/storagesuccess.png)
    * Create an Azure Blob container. Type in Shell
    	```
		New-AzureStorageContainer -Name $defaultStorageContainerName -Context $destContext
	```
		
    * Create an HDInsight cluster
    	* Step 1. Creating the credentials.
	```
	$credentials = Get-Credential -Message "Enter Cluster user credentials" -UserName "admin"
	$sshCredentials = Get-Credential -Message "Enter SSH user credentials"
	```
	* Step 2. The location of the HDInsight cluster must be in the same data center as the Storage account.
	```
	$location = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $defaultStorageAccountName | %{$_.Location}
	```
	* Step 3. Creating the HDInsight Cluster. Please be patient, It can take up to 20 minutes to create a cluster.
	
	```
	New-AzureRmHDInsightCluster `
    	-ClusterName $clusterName `
    	-ResourceGroupName $resourceGroupName `
    	-HttpCredential $credentials `
    	-Location $location `
    	-DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
    	-DefaultStorageAccountKey $defaultStorageAccountKey `
	-DefaultStorageContainer $defaultStorageContainerName  `
	-ClusterSizeInNodes $clusterNodes `
    	-ClusterType Hadoop `
	-OSType Linux `
    	-Version "3.4" `
	-SshCredential $sshCredentials
	```
	
    		
	
