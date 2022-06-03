# NuGet packages
* [SharePointHelper](https://www.nuget.org/packages/SharePointHelper/)
* [SharePointHelper.Core.3.1](https://www.nuget.org/packages/SharePointHelper.Core.3.1/)


I have built these packages to help you with a wrapper around [Microsoft.Graph](https://docs.microsoft.com/en-us/graph/overview) to do certain functionalities on SharePoint using C# .NET code easily  

# Features supported 

*	`Task<DriveItem> CreateFolder(AzureConfiguration configuration, string uri, string folderName);` 
It helps you create a folder in a `uri` provided. It ensures that, if the folder doesn't exist already, it creates a new one, ignore it otherwise.

*	`Task SafeCreateDirectory(AzureConfiguration configuration, string uri);` 
Creates the passed `uri` in the sharepoint site. Say for instance in Example: `/RootFolder/Folder1/Folder2` if the`Folder1` doesn't exist, it creates it first and then create `Folder2` under it	 

*	`Task<string> DownloadFile(AzureConfiguration configuration, string fileId);` 
Downloads the file as `.docx` format and returns the download location

*	` Task<DriveItem> MoveFile(AzureConfiguration configuration, string destinationUri, string destinationFileName, string sourceUri, string sourceFileName);` Moves source file by grabbing it from its `sourceUri` and `sourceFileName` to the destination location identified by its `destinationUri`  

*	`Task<DriveItem> CopyFile(AzureConfiguration configuration, string destinationUri, string destinationFileName, string sourceUri, string sourceFileName);` Copies source file by grabbing it from its `sourceUri` and `sourceFileName` to the destination location identified by its `destinationUri` 

# Quickstarter
You can just download the solution zip from this repository and make changes based on your needs

# Usage

```csharp
using SharePointHelper;

namespace TestLibrary
{
    public class YourClass 
    {
       private async Task MyMethod()
        {
            
           AzureConfiguration configuration = new AzureConfiguration(
                "Azure ClientId", "Azure ClientSecret", "Azure TenantId", "SharePoint SiteName", "SharePoint site's endPoint");

            // Example:
            // Endpoint "https://dummyorganization.sharepoint.com"

            // "https://dummyorganization.sharepoint.com/sites/TestingSite"
            // SiteName "TestingSite" 



            SharePointService sharePointService = new SharePointService();
            
            
            DriveItem newFolderDriveItem = await sharePointService.CreateFolder(configuration, "/root/Folder1/Folder2", "Folder3");

            string downloadedPath = await sharePointService.DownloadFile(configuration, "XXXX");

            await sharePointService.SafeCreateDirectory(configuration,"/root/FolderA/FolderB");

            DriveItem movedDriveItem = await sharePointService.MoveFile(configuration,
                "/root/Folder1/dst", "dst.docx",
                "/root/Folder1/src", "src.docx");

            DriveItem copiedDriveItem = await sharePointService.CopyFile(configuration,
                "/root/Folder1/dst", "dst.docx",
                "/root/Folder1/src", "src.docx");
        }
    }
}
```

# If you liked my work
<a href="https://www.buymeacoffee.com/pradeepradyumna" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-red.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>  

