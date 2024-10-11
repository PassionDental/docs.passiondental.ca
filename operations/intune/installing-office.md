# Microsoft Office at Passion Dental Group

## Overview

We are in the process of signing an Enterprise License Agreement (ELA) with Microsoft. Once we do, we plan to use shared device licensing via Office 365. Until then, we alos have a volume license approach available. Please see below for options on that:

### Volume License Install Instructions

* Download a copy of our configuration and office deployment tool from here: `\\pgfs01.ad.passiondental.ca\IT\install_media\Office\passion_volume_license.zip`
* Extract the files
* Open a powershell window
* `cd` to the path of the extracted files
* Run `.\setup.exe /configure .\Passion_Volume_License.xml`
* It will take a while...
* When the command completes in Powershell, the installation was successful. 

Note: our configuration install the following office Products: Word, Powerpoint, Excel, and Outlook. If you need other office features, please reach out to IT at support@passiondental.ca

### Passion Install Office on for shared device licensing

We are still working out licensing requirements for device based licensing. Stay tuned!

### Install Office using Microsoft Apps for Enterprise (User Licensing)

We have a Smartsheet setup to automatically create the users and appropriately license them. That Smartsheet can be found here: https://app.smartsheet.com/sheets/h5c24vMQJ3C8H79QcX8hc6vPQFgmPjw5vfx3qJ71?view=grid

Once you have the user credentials for the service account licensed for Microsoft Office, you're ready to install it on the target computer.

First, you will need a copy of the Office Deployment tool downloaded. You can find it on our file share at `\\pgfs01.ad.passiondental.ca\IT\install_media\Office\Office Deployment Tool` or by visiting <a href="https://www.microsoft.com/en-us/download/details.aspx?id=49117" target="_blank">Microsoft's website</a>.

Steps:

* Once you have your `setup.exe` and `AppsForEnterprise.xml` files in your working directory, type `.\setup.exe /configure .\AppsForEnterprise.xml`
  * If the current account is not an administrator, you may be prompted for admin credentials
* Once the install completes, you need to open an application, like Microsoft Word
* Go activate office using the account information from the Smartsheet above.
  * Note: Once office is activated, it should work on all accounts because we use `SharedComputerLicensing` in our configuration file.

If you need to create the XML file yourself, here is a copy of the configuration:
````xml
<Configuration ID="99bb3e57-34ce-447b-a2d1-22a74ed2beda">
  <Info Description="" />
  <Add OfficeClientEdition="64" Channel="MonthlyEnterprise" MigrateArch="TRUE">
    <Product ID="O365ProPlusEEANoTeamsRetail">
      <Language ID="en-us" />
      <ExcludeApp ID="Access" />
      <ExcludeApp ID="Groove" />
      <ExcludeApp ID="Lync" />
      <ExcludeApp ID="OneDrive" />
      <ExcludeApp ID="Publisher" />
      <ExcludeApp ID="Bing" />
    </Product>
  </Add>
  <Property Name="SharedComputerLicensing" Value="1" />
  <Property Name="FORCEAPPSHUTDOWN" Value="TRUE" />
  <Property Name="DeviceBasedLicensing" Value="0" />
  <Property Name="SCLCacheOverride" Value="0" />
  <Updates Enabled="TRUE" />
  <RemoveMSI />
  <AppSettings>
    <Setup Name="Company" Value="Passion Dental" />
  </AppSettings>
  <Display Level="None" AcceptEULA="TRUE" />
</Configuration>
```` 