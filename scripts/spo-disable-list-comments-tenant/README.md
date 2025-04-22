

# Disable SharePoint List Commenting at tenant level

## Summary

This sample script shows how to disable commenting feature in SharePoint online lists at tenant level.

Scenario inspired from this blog post: [How to Enable/Disable the commenting in SharePoint Online/Microsoft Lists](https://ganeshsanapblogs.wordpress.com/2021/01/09/how-to-enable-disable-the-commenting-in-sharepoint-online-microsoft-lists/)

![Outupt Screenshot](assets/output.png)

# [SPO Management Shell](#tab/spoms-ps)

```powershell

# SharePoint online admin site url
$siteUrl = "https://<tenant>-admin.sharepoint.com/"	

# Connect to SharePoint Online site
Connect-SPOService -Url $siteUrl

# To disable comments on list items
Set-SPOTenant -CommentsOnListItemsDisabled $true

# To enable comments on list items
Set-SPOTenant -CommentsOnListItemsDisabled $false

```

[!INCLUDE [More about SPO Management Shell](../../docfx/includes/MORE-SPOMS.md)]

# [PnP PowerShell](#tab/pnpps)

```powershell

# SharePoint online admin site url
$siteUrl = "https://<tenant>-admin.sharepoint.com/"	

# Connect to SharePoint Online site
Connect-PnPOnline -Url $siteUrl -Interactive

# To disable comments on list items
Set-PnPTenant -CommentsOnListItemsDisabled $true

# To enable comments on list items
Set-PnPTenant -CommentsOnListItemsDisabled $false

```

[!INCLUDE [More about PnP PowerShell](../../docfx/includes/MORE-PNPPS.md)]

# [CLI for Microsoft 365](#tab/cli-m365-ps)

```powershell

# Get Credentials to connect
$m365Status = m365 status
if ($m365Status -match "Logged Out") {
   m365 login
}

# To disable comments on list items
m365 spo tenant settings set --CommentsOnListItemsDisabled true

# To enable comments on list items
m365 spo tenant settings set --CommentsOnListItemsDisabled false

```

[!INCLUDE [More about CLI for Microsoft 365](../../docfx/includes/MORE-CLIM365.md)]

***

## Contributors

| Author(s) |
|-----------|
| [Ganesh Sanap](https://ganeshsanapblogs.wordpress.com/about) |

[!INCLUDE [DISCLAIMER](../../docfx/includes/DISCLAIMER.md)]
<img src="https://m365-visitor-stats.azurewebsites.net/script-samples/scripts/spo-disable-list-comments-tenant" aria-hidden="true" />
