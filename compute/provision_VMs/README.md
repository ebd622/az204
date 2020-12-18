(Under Construction)

# Work with VMs

#### 1. Connect

<details><summary>PowerShell</summary>
<p>

```bash
Connect-AzAccount
```

</p>
</details>

<details><summary>Azure CLI</summary>
<p>

```bash
kubectl create namespace mynamespace
kubectl run nginx --image=nginx --restart=Never -n mynamespace
```

</p>
</details>


```
Connect-AzAccount
```

#### 2.
```
Get-AzVm
```

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
