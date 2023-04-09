# PowerShell Scripts to Install/Uninstall HttpPlatformHandler for IIS Express

> * Learn how to install CORS module from [this sibling project](https://github.com/lextm/iisexpress-cors).
> * Learn how to patch ASP.NET Core module on Windows 11 ARM64 from [this sibling project](https://github.com/lextm/ancm-arm64).
> * Learn how to use IIS Express with Visual Studio Code from [this sibling project](https://github.com/jexuswebserver/vscode-iis).

## Install

1. Install [IIS Express](https://learn.microsoft.com/iis/extensions/introduction-to-iis-express/iis-express-overview#installing-iis-express).
1. Download [Microsoft HttpPlatformHandler for IIS](https://www.iis.net/downloads/microsoft/httpplatformhandler) installer.
1. Install [lessmsi](https://github.com/activescott/lessmsi) tool and configure it in your PATH (so that `lessmsi` can be called by the install script).
1. Run the proper command to install HttpPlatformHandler to IIS Express,

   > If HttpPlatformHandler for IIS has been installed on this same machine in advance, then `-msiFile` switch can be omitted.
   > 
   > **For VS 2015 and above, you must use `-fileName` switch to guide the script and modify the correct `applicationHost.config` file for your Visual Studio solution file.** To learn more on how to locate the correct config file, you can [read this article](https://docs.jexusmanager.com/getting-started/features.html#add-iis-express-from-visual-studio-2015-2017-2019-solution-file).

   * At command prompt
   ``` cmd
   powershell.exe -file install.ps1 -msiFile httpPlatformHandler_amd64.msi
   ```
   * In PowerShell console   
   ``` powershell
   .\install.ps1 -msiFile httpPlatformHandler_amd64.msi
   ```

   > If `-msiFile` is omitted, the install script tries to copy the files from local IIS installation folders. Make sure you have installed HttpPlatformHandler on IIS, or errors are expected.

The configuration on IIS Express is exactly the same as IIS, and just make sure you are editing the right config files,

https://learn.microsoft.com/iis/extensions/httpplatformhandler/httpplatformhandler-configuration-reference

## Uninstall
1. Run `uninstall.ps1` to uninstall HttpPlatformHandler from IIS Express.

## Notes

* The current release only supports Windows x64 machines.
* The scripts must be run as administrator, because they need to copy/remove files to/from Program Files folder.
* **`install.ps1` and `uninstall.ps1` only manipulate the default IIS Express config file in current user's My Documents folder.**
* **If a custom config file needs to be modified, run the PowerShell scripts with arguments (like `install.ps1 -fileName custom.config`).**
