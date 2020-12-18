(Under Construction)

# Work with VMs

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
Connect-AzAccount
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
todo
```

</p>
</details>


#### 3. Create a new resource group `pwshellgr`
```
New-AzResourceGroup -Name pwshellgr -Location "West Europe"
```

#### 4. Create VM
The command will create and run a VM:
```
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


#### 5. Get status of VM (should be `running`)
```
Get-AzVm -Status
```

#### 6. Stop the VM
```
Stop-AzVM -ResourceGroupName "pwshellgr" -Name "aznewvm"
```

#### 7. Check a status of VM (should be `deallocated`)
```
Get-AzVm -Status
```

#### 8. Remove the resource group (including all resources)
```
Remove-AzResourceGroup -Name "pwshellgr"
```
