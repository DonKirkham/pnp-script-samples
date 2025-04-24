

# Hide the 'See All' Button in the Highlighted Content Web Part

## Summary

Recently, I encountered an issue with the "Show title and commands" toggle in the out-of-the-box Highlighted Content web part. It stopped working on both my development and customer tenant. 

![ToggleOff](assets/HighlightWebPart.png)

While awaiting a resolution from Microsoft, I decided to find a workaround. That's when the PnP PowerShell cmdlet `Set-PnPPageWebPart` came to the rescue. The solution involves updating the **PropertiesJson** property of the web part.
 
# [PnP PowerShell](#tab/pnpps)

```PowerShell

# Connect to your SharePoint site
Connect-PnPOnline -Url "https://contoso.sharepoint.com/sites/Project" -Interactive

# Specify the page URL
$pageUrl = "ProjectHome.aspx"

# Get the page and its web parts
$page = Get-PnPClientSidePage -Identity $pageUrl
$webParts = $page.Controls | Where-Object { $_.Title -eq 'Highlighted content' } 

# Loop through each web part
foreach ($webPart in $webParts) {
        # Update isTitleEnabled property within PropertiesJson
        $jsonUp = $webpart.PropertiesJson.Replace('"isTitleEnabled":true','"isTitleEnabled":false') 
        
        Set-PnPPageWebPart -Page $pageUrl -Identity $webPart.InstanceId -PropertiesJson $jsonUp
    }

# Disconnect from the SharePoint site
Disconnect-PnPOnline

```

[!INCLUDE [More about PnP PowerShell](../../docfx/includes/MORE-PNPPS.md)]

## Source Credit

Sample first appeared on [How to Hide the 'See All' Button in the Highlighted Content Web Part using PnP PowerShell](https://reshmeeauckloo.com/posts/powershell_highlightwebpart_hideseeall/)

## Contributors

| Author(s) |
|-----------|
| [Reshmee Auckloo](https://github.com/reshmee011)|

[!INCLUDE [DISCLAIMER](../../docfx/includes/DISCLAIMER.md)]

<img src="https://m365-visitor-stats.azurewebsites.net/script-samples/scripts/spo-update-highlightcontentwebpart-seeall" aria-hidden="true" />
