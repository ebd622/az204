(Under Construction)

# Work with VMs

Az PowerShell Module Reference: https://docs.microsoft.com/en-us/powershell/module/?view=azps-5.2.0

Azure CLI commands: https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest#az_vm_create




#### 1. Connect to Azure with an authenticated account

<details><summary>Using PowerShell:</summary>
<p>
  
```bash
Connect-AzAccount
```

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az login
```

</p>
</details>


#### 2. Gets the properties of a virtual machine(s)
<details><summary>Using PowerShell:</summary>
<p>
  
```bash
Get-AzVm
```

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az vm list
az vm list -d -o table
```

</p>
</details>


#### 3. Create a new resource group
<details><summary>Using PowerShell:</summary>
<p>
  
```bash
New-AzResourceGroup -Name pwshellgr -Location "West Europe"
```

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az group create --name cligroup --location "West Europe"
```

</p>
</details>


#### 4. Create VM
<details><summary>Using PowerShell:</summary>
<p>
  
```bash
New-AzVm `
-ResourceGroupName pwshellgr `
-Name aznewvm `
-Location "West Europe" `
-VirtualNetworkName "mynewVNet" `
-SubnetName "default" `
-SecurityGroupName "mynewNSG" `
-PublicIpAddressName "mypublicip" `
-OpenPorts 80,3389
```
You will need to provide `user` and `password` for a new VM.

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az vm create \
--resource-group cligroup \
--name aznewvm2 \
--image win2016datacenter \
--admin-username azadmin \
--admin-password xxxxxxxx
```

</p>
</details>



#### 5. Get status of VM (should be `running`)
<details><summary>Using PowerShell:</summary>
<p>
  
```bash
Get-AzVm -Status
```

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az vm list
az vm list -d -o table
az vm list -d -o table --query "[?name=='aznewvm2']"
```

</p>
</details>


#### 6. Stop the VM
<details><summary>Using PowerShell:</summary>
<p>
  
```bash
Stop-AzVM -ResourceGroupName "pwshellgr" -Name "aznewvm"
```

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az vm stop --resource-group cligroup --name aznewvm2
```

</p>
</details>


#### 7. Check a status of VM (should be `deallocated`)
<details><summary>Using PowerShell:</summary>
<p>
  
```bash
Get-AzVm -Status
```

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az vm list -d -o table --query "[?name=='aznewvm2']"
```

</p>
</details>


#### 8. Remove the resource group (including all resources)
<details><summary>Using PowerShell:</summary>
<p>
  
```bash
Remove-AzResourceGroup -Name "pwshellgr"
```

</p>
</details>

<details><summary>Using Azure CLI:</summary>
<p>
  
```bash
az vm delete -resource-group cligroup 
```

</p>
</details>

