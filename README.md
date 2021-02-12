# WVD-AZones
ARM template to deploy WVD in Availability Zones.

This template for WVD Classic will distribute your WVD Session Host VM's equally across all three Azure Availability Zones in the region (where supported) into which you are deploying.

This is by the addition of this code in the standard WVD deployment template:

        {
            "condition": "[variables('rdshManagedDisks')]",
            "apiVersion": "2018-10-01",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(if(variables('rdshManagedDisks'), '', 'null'), variables('rdshPrefix'), copyindex())]",
            "zones": [
                "[add(1,mod(copyindex(),3))]"
            ],
            "location": "[parameters('location')]",
            "copy": {
                "name": "rdsh-vm-loop",
                "count": "[parameters('rdshNumberOfInstances')]"
            },

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FTomHickling%2FWVD-AZones%2Fmaster%2FmainTemplate.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FTomHickling%2FWVD-AZones%2Fmaster%2FmainTemplate.jsonn" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>
