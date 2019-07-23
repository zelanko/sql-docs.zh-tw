---
title: 檢視與讀取 SQL Server 安裝程式記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7bf7d199239be10760df49d586cdf5048fbc4a80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906774"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>檢視與讀取 SQL Server 安裝程式記錄檔

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安裝程式預設會將記錄檔建立在 **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** 內具有日期和時間戳記的資料夾中，*nnn* 為對應至要安裝之 SQL 版本的數字。 時間戳記記錄檔資料夾的名稱格式為 YYYYMMDD_hhmmss。 在自動安裝模式下執行安裝程式時，會在 %temp%\sqlsetup*.log 內建立記錄檔。 記錄檔資料夾中的所有檔案都會封存到個別記錄檔資料夾的 Log\*.cab 檔中。  

   | 檔案           | 路徑 |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI Log Files** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **For unattended installations** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > The numbers in the path *nnn* correspond to the version of SQL being installed. In the above picture, SQL 2017 was installed, so the folder is 140. For SQL 2016, the folder would be 130, and for SQL 2014 the folder would be 120.
  
 SQL server setup completes three basic phases: 
  
1.  Global Rules verification: validates basic system requirements
2.  Component update: checks to see if there are any updates available for the media being installed
3.  User-requested action: allows the user to select and customize features
  

This workflow produces a single summary log, and either a single detail log for a base SQL Server installation, or two detail logs for when update, such as a service pack, is installed along with the base installation. 
  
Additionally, there are datastore files that contain a snapshot of the state of all the configuration objects that are being tracked by the setup process, and are useful for troubleshooting configuration errors. XML dump files are created for each execution phase and are saved in the Datastore log subfolder under the time-stamped log folder. 

The following sections describe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup log files.  
  
## Summary.txt file 
  
### Overview  
 This file shows the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that were detected during Setup, the operating system environment, command-line parameter values if they are specified, and the overall status of each MSI/MSP that was executed.
  
 The log is organized into the following sections:
  
-   An overall summary of the execution  
-   Properties and the configuration of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup was run  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] product features previously installed on the computer  
-   Description of the installation version and installation package properties
-   Runtime input settings that are provided during install  
-   Location of the configuration file  
-   Details of the execution results  
-   Global rules  
-   Rules specific to the installation scenario  
-   Failed rules  
-   Location of the rules report file


  >[!NOTE]
  > Note that when patching there can be a number of sub folders (one for each instance being patched, and one for shared features) which contain a similiar set of files (i.e. %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### Location  
 The summary.txt is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 To find errors in the summary text file, search the file by using the "error" or "failed" keywords.
  
## Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### Overview  
 The summary_engine base file is similar to the summary file and is generated during the main workflow.
  
### Location  
 The Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## Detail.txt file
  
### Overview
 Detail.txt is generated for the main workflow such as install or upgrade, and provides the details of the execution. The logs in the file are generated based on the time when each action for the installation was invoked. The text file shows the order in which the actions were executed, as well as their dependencies.  
  
### Location  
 The detail.txt file is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 If an error occurs during the Setup process, the exception or error is logged at the end of this file. To find the errors in this file, first examine the end of the file followed by a search of the file for the "error" or "exception" keywords
    
## MSI log files
  
### Overview  
 The MSI log files provide details of the installation package process. They are generated by the MSIEXEC during the installation of the specified package.  
  
 Types of MSI log files:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### Location  
 The MSI log files are located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 At the end of the file is a summary of the execution, which includes the success or failure status and properties. To find the error in the MSI file, search for "value 3" and review the text before and after.  
  
## ConfigurationFile.ini file
  
### Overview  
 The configuration file contains the input settings that are provided during installation. It can be used to restart the installation without having to enter the settings manually. However, passwords for the accounts, PID, and some parameters are not saved in the configuration file. The settings can be either added to the file or provided by using the command line or the Setup user interface. For more information, see [Install SQL Server 2016 Using a Configuration File](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Location  
 The ConfigurationFile.ini is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm file
  
### Overview  
 The system configuration check report contains a short description for each executed rule, and the execution status.
  
### Location  
The SystemConfigurationCheck_Report.htm is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## See also  
 [Install SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)\`programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Logft Docs"
ms.custom: ""
ms.date: "09/09/2016"
ms.prod: sql
ms.reviewer: ""
ms.technology: install
ms.topic: conceptual
helpviewer_keywords: 
  - "viewing logs"
  - "displaying log files"
  - "Setup [SQL Server], logs"
  - "installation log files [SQL Server]"
  - "installing SQL Server, logs"
  - "errors [SQL Server], Setup"
  - "logs [SQL Server], Setup"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# View and Read SQL Server Setup Log Files

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Setup creates log files in a dated and time-stamped folder within **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** by default, where *nnn* are numbers that correspond to the version of SQL that's being installed. The time-stamped log folder name format is YYYYMMDD_hhmmss. When Setup is executed in unattended mode, the logs are created within %temp%\sqlsetup*.log. All files in the log folder are archived into the Log\*.cab file in their respective log folder.  

   | File           | Path |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI Log Files** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **For unattended installations** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > The numbers in the path *nnn* correspond to the version of SQL being installed. In the above picture, SQL 2017 was installed, so the folder is 140. For SQL 2016, the folder would be 130, and for SQL 2014 the folder would be 120.
  
 SQL server setup completes three basic phases: 
  
1.  Global Rules verification: validates basic system requirements
2.  Component update: checks to see if there are any updates available for the media being installed
3.  User-requested action: allows the user to select and customize features
  

This workflow produces a single summary log, and either a single detail log for a base SQL Server installation, or two detail logs for when update, such as a service pack, is installed along with the base installation. 
  
Additionally, there are datastore files that contain a snapshot of the state of all the configuration objects that are being tracked by the setup process, and are useful for troubleshooting configuration errors. XML dump files are created for each execution phase and are saved in the Datastore log subfolder under the time-stamped log folder. 

The following sections describe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup log files.  
  
## Summary.txt file 
  
### Overview  
 This file shows the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that were detected during Setup, the operating system environment, command-line parameter values if they are specified, and the overall status of each MSI/MSP that was executed.
  
 The log is organized into the following sections:
  
-   An overall summary of the execution  
-   Properties and the configuration of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup was run  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] product features previously installed on the computer  
-   Description of the installation version and installation package properties
-   Runtime input settings that are provided during install  
-   Location of the configuration file  
-   Details of the execution results  
-   Global rules  
-   Rules specific to the installation scenario  
-   Failed rules  
-   Location of the rules report file


  >[!NOTE]
  > Note that when patching there can be a number of sub folders (one for each instance being patched, and one for shared features) which contain a similiar set of files (i.e. %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### Location  
 The summary.txt is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 To find errors in the summary text file, search the file by using the "error" or "failed" keywords.
  
## Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### Overview  
 The summary_engine base file is similar to the summary file and is generated during the main workflow.
  
### Location  
 The Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## Detail.txt file
  
### Overview
 Detail.txt is generated for the main workflow such as install or upgrade, and provides the details of the execution. The logs in the file are generated based on the time when each action for the installation was invoked. The text file shows the order in which the actions were executed, as well as their dependencies.  
  
### Location  
 The detail.txt file is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 If an error occurs during the Setup process, the exception or error is logged at the end of this file. To find the errors in this file, first examine the end of the file followed by a search of the file for the "error" or "exception" keywords
    
## MSI log files
  
### Overview  
 The MSI log files provide details of the installation package process. They are generated by the MSIEXEC during the installation of the specified package.  
  
 Types of MSI log files:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### Location  
 The MSI log files are located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 At the end of the file is a summary of the execution, which includes the success or failure status and properties. To find the error in the MSI file, search for "value 3" and review the text before and after.  
  
## ConfigurationFile.ini file
  
### Overview  
 The configuration file contains the input settings that are provided during installation. It can be used to restart the installation without having to enter the settings manually. However, passwords for the accounts, PID, and some parameters are not saved in the configuration file. The settings can be either added to the file or provided by using the command line or the Setup user interface. For more information, see [Install SQL Server 2016 Using a Configuration File](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Location  
 The ConfigurationFile.ini is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm file
  
### Overview  
 The system configuration check report contains a short description for each executed rule, and the execution status.
  
### Location  
The SystemConfigurationCheck_Report.htm is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## See also  
 [Install SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)\`programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmssom: ""
ms.date: "09/09/2016"
ms.prod: sql
ms.reviewer: ""
ms.technology: install
ms.topic: conceptual
helpviewer_keywords: 
  - "viewing logs"
  - "displaying log files"
  - "Setup [SQL Server], logs"
  - "installation log files [SQL Server]"
  - "installing SQL Server, logs"
  - "errors [SQL Server], Setup"
  - "logs [SQL Server], Setup"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# View and Read SQL Server Setup Log Files

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Setup creates log files in a dated and time-stamped folder within **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** by default, where *nnn* are numbers that correspond to the version of SQL that's being installed. The time-stamped log folder name format is YYYYMMDD_hhmmss. When Setup is executed in unattended mode, the logs are created within %temp%\sqlsetup*.log. All files in the log folder are archived into the Log\*.cab file in their respective log folder.  

   | File           | Path |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI Log Files** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **For unattended installations** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > The numbers in the path *nnn* correspond to the version of SQL being installed. In the above picture, SQL 2017 was installed, so the folder is 140. For SQL 2016, the folder would be 130, and for SQL 2014 the folder would be 120.
  
 SQL server setup completes three basic phases: 
  
1.  Global Rules verification: validates basic system requirements
2.  Component update: checks to see if there are any updates available for the media being installed
3.  User-requested action: allows the user to select and customize features
  

This workflow produces a single summary log, and either a single detail log for a base SQL Server installation, or two detail logs for when update, such as a service pack, is installed along with the base installation. 
  
Additionally, there are datastore files that contain a snapshot of the state of all the configuration objects that are being tracked by the setup process, and are useful for troubleshooting configuration errors. XML dump files are created for each execution phase and are saved in the Datastore log subfolder under the time-stamped log folder. 

The following sections describe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup log files.  
  
## Summary.txt file 
  
### Overview  
 This file shows the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that were detected during Setup, the operating system environment, command-line parameter values if they are specified, and the overall status of each MSI/MSP that was executed.
  
 The log is organized into the following sections:
  
-   An overall summary of the execution  
-   Properties and the configuration of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup was run  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] product features previously installed on the computer  
-   Description of the installation version and installation package properties
-   Runtime input settings that are provided during install  
-   Location of the configuration file  
-   Details of the execution results  
-   Global rules  
-   Rules specific to the installation scenario  
-   Failed rules  
-   Location of the rules report file


  >[!NOTE]
  > Note that when patching there can be a number of sub folders (one for each instance being patched, and one for shared features) which contain a similiar set of files (i.e. %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### Location  
 The summary.txt is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 To find errors in the summary text file, search the file by using the "error" or "failed" keywords.
  
## Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### Overview  
 The summary_engine base file is similar to the summary file and is generated during the main workflow.
  
### Location  
 The Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## Detail.txt file
  
### Overview
 Detail.txt is generated for the main workflow such as install or upgrade, and provides the details of the execution. The logs in the file are generated based on the time when each action for the installation was invoked. The text file shows the order in which the actions were executed, as well as their dependencies.  
  
### Location  
 The detail.txt file is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 If an error occurs during the Setup process, the exception or error is logged at the end of this file. To find the errors in this file, first examine the end of the file followed by a search of the file for the "error" or "exception" keywords
    
## MSI log files
  
### Overview  
 The MSI log files provide details of the installation package process. They are generated by the MSIEXEC during the installation of the specified package.  
  
 Types of MSI log files:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### Location  
 The MSI log files are located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 At the end of the file is a summary of the execution, which includes the success or failure status and properties. To find the error in the MSI file, search for "value 3" and review the text before and after.  
  
## ConfigurationFile.ini file
  
### Overview  
 The configuration file contains the input settings that are provided during installation. It can be used to restart the installation without having to enter the settings manually. However, passwords for the accounts, PID, and some parameters are not saved in the configuration file. The settings can be either added to the file or provided by using the command line or the Setup user interface. For more information, see [Install SQL Server 2016 Using a Configuration File](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Location  
 The ConfigurationFile.ini is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm file
  
### Overview  
 The system configuration check report contains a short description for each executed rule, and the execution status.
  
### Location  
The SystemConfigurationCheck_Report.htm is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## See also  
 [Install SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)\`programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmssom: ""
ms.date: "09/09/2016"
ms.prod: sql
ms.reviewer: ""
ms.technology: install
ms.topic: conceptual
helpviewer_keywords: 
  - "viewing logs"
  - "displaying log files"
  - "Setup [SQL Server], logs"
  - "installation log files [SQL Server]"
  - "installing SQL Server, logs"
  - "errors [SQL Server], Setup"
  - "logs [SQL Server], Setup"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# View and Read SQL Server Setup Log Files

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Setup creates log files in a dated and time-stamped folder within **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** by default, where *nnn* are numbers that correspond to the version of SQL that's being installed. The time-stamped log folder name format is YYYYMMDD_hhmmss. When Setup is executed in unattended mode, the logs are created within %temp%\sqlsetup*.log. All files in the log folder are archived into the Log\*.cab file in their respective log folder.  

   | File           | Path |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI Log Files** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **For unattended installations** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > The numbers in the path *nnn* correspond to the version of SQL being installed. In the above picture, SQL 2017 was installed, so the folder is 140. For SQL 2016, the folder would be 130, and for SQL 2014 the folder would be 120.
  
 SQL server setup completes three basic phases: 
  
1.  Global Rules verification: validates basic system requirements
2.  Component update: checks to see if there are any updates available for the media being installed
3.  User-requested action: allows the user to select and customize features
  

This workflow produces a single summary log, and either a single detail log for a base SQL Server installation, or two detail logs for when update, such as a service pack, is installed along with the base installation. 
  
Additionally, there are datastore files that contain a snapshot of the state of all the configuration objects that are being tracked by the setup process, and are useful for troubleshooting configuration errors. XML dump files are created for each execution phase and are saved in the Datastore log subfolder under the time-stamped log folder. 

The following sections describe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup log files.  
  
## Summary.txt file 
  
### Overview  
 This file shows the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that were detected during Setup, the operating system environment, command-line parameter values if they are specified, and the overall status of each MSI/MSP that was executed.
  
 The log is organized into the following sections:
  
-   An overall summary of the execution  
-   Properties and the configuration of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup was run  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] product features previously installed on the computer  
-   Description of the installation version and installation package properties
-   Runtime input settings that are provided during install  
-   Location of the configuration file  
-   Details of the execution results  
-   Global rules  
-   Rules specific to the installation scenario  
-   Failed rules  
-   Location of the rules report file


  >[!NOTE]
  > Note that when patching there can be a number of sub folders (one for each instance being patched, and one for shared features) which contain a similiar set of files (i.e. %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### Location  
 The summary.txt is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 To find errors in the summary text file, search the file by using the "error" or "failed" keywords.
  
## Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### Overview  
 The summary_engine base file is similar to the summary file and is generated during the main workflow.
  
### Location  
 The Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## Detail.txt file
  
### Overview
 Detail.txt is generated for the main workflow such as install or upgrade, and provides the details of the execution. The logs in the file are generated based on the time when each action for the installation was invoked. The text file shows the order in which the actions were executed, as well as their dependencies.  
  
### Location  
 The detail.txt file is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 If an error occurs during the Setup process, the exception or error is logged at the end of this file. To find the errors in this file, first examine the end of the file followed by a search of the file for the "error" or "exception" keywords
    
## MSI log files
  
### Overview  
 The MSI log files provide details of the installation package process. They are generated by the MSIEXEC during the installation of the specified package.  
  
 Types of MSI log files:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### Location  
 The MSI log files are located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 At the end of the file is a summary of the execution, which includes the success or failure status and properties. To find the error in the MSI file, search for "value 3" and review the text before and after.  
  
## ConfigurationFile.ini file
  
### Overview  
 The configuration file contains the input settings that are provided during installation. It can be used to restart the installation without having to enter the settings manually. However, passwords for the accounts, PID, and some parameters are not saved in the configuration file. The settings can be either added to the file or provided by using the command line or the Setup user interface. For more information, see [Install SQL Server 2016 Using a Configuration File](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Location  
 The ConfigurationFile.ini is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm file
  
### Overview  
 The system configuration check report contains a short description for each executed rule, and the execution status.
  
### Location  
The SystemConfigurationCheck_Report.htm is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## See also  
 [Install SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)\`programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastoredate: "09/09/2016"
ms.prod: sql
ms.reviewer: ""
ms.technology: install
ms.topic: conceptual
helpviewer_keywords: 
  - "viewing logs"
  - "displaying log files"
  - "Setup [SQL Server], logs"
  - "installation log files [SQL Server]"
  - "installing SQL Server, logs"
  - "errors [SQL Server], Setup"
  - "logs [SQL Server], Setup"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# View and Read SQL Server Setup Log Files

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Setup creates log files in a dated and time-stamped folder within **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** by default, where *nnn* are numbers that correspond to the version of SQL that's being installed. The time-stamped log folder name format is YYYYMMDD_hhmmss. When Setup is executed in unattended mode, the logs are created within %temp%\sqlsetup*.log. All files in the log folder are archived into the Log\*.cab file in their respective log folder.  

   | File           | Path |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI 記錄檔** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **For unattended installations** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > The numbers in the path *nnn* correspond to the version of SQL being installed. In the above picture, SQL 2017 was installed, so the folder is 140. For SQL 2016, the folder would be 130, and for SQL 2014 the folder would be 120.
  
 SQL server setup completes three basic phases: 
  
1.  Global Rules verification: validates basic system requirements
2.  Component update: checks to see if there are any updates available for the media being installed
3.  User-requested action: allows the user to select and customize features
  

This workflow produces a single summary log, and either a single detail log for a base SQL Server installation, or two detail logs for when update, such as a service pack, is installed along with the base installation. 
  
Additionally, there are datastore files that contain a snapshot of the state of all the configuration objects that are being tracked by the setup process, and are useful for troubleshooting configuration errors. XML dump files are created for each execution phase and are saved in the Datastore log subfolder under the time-stamped log folder. 

The following sections describe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup log files.  
  
## Summary.txt file 
  
### Overview  
 This file shows the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that were detected during Setup, the operating system environment, command-line parameter values if they are specified, and the overall status of each MSI/MSP that was executed.
  
 The log is organized into the following sections:
  
-   An overall summary of the execution  
-   Properties and the configuration of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup was run  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] product features previously installed on the computer  
-   Description of the installation version and installation package properties
-   Runtime input settings that are provided during install  
-   Location of the configuration file  
-   Details of the execution results  
-   Global rules  
-   Rules specific to the installation scenario  
-   Failed rules  
-   Location of the rules report file


  >[!NOTE]
  > Note that when patching there can be a number of sub folders (one for each instance being patched, and one for shared features) which contain a similiar set of files (i.e. %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### Location  
 The summary.txt is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 To find errors in the summary text file, search the file by using the "error" or "failed" keywords.
  
## Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### Overview  
 The summary_engine base file is similar to the summary file and is generated during the main workflow.
  
### Location  
 The Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## Detail.txt file
  
### Overview
 Detail.txt is generated for the main workflow such as install or upgrade, and provides the details of the execution. The logs in the file are generated based on the time when each action for the installation was invoked. The text file shows the order in which the actions were executed, as well as their dependencies.  
  
### Location  
 The detail.txt file is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 If an error occurs during the Setup process, the exception or error is logged at the end of this file. To find the errors in this file, first examine the end of the file followed by a search of the file for the "error" or "exception" keywords
    
## MSI log files
  
### Overview  
 The MSI log files provide details of the installation package process. They are generated by the MSIEXEC during the installation of the specified package.  
  
 Types of MSI log files:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### Location  
 The MSI log files are located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 At the end of the file is a summary of the execution, which includes the success or failure status and properties. To find the error in the MSI file, search for "value 3" and review the text before and after.  
  
## ConfigurationFile.ini file
  
### Overview  
 The configuration file contains the input settings that are provided during installation. It can be used to restart the installation without having to enter the settings manually. However, passwords for the accounts, PID, and some parameters are not saved in the configuration file. The settings can be either added to the file or provided by using the command line or the Setup user interface. For more information, see [Install SQL Server 2016 Using a Configuration File](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Location  
 The ConfigurationFile.ini is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm file
  
### Overview  
 The system configuration check report contains a short description for each executed rule, and the execution status.
  
### Location  
The SystemConfigurationCheck_Report.htm is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## See also  
 [Install SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)\`programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.loge: "09/09/2016"
ms.prod: sql
ms.reviewer: ""
ms.technology: install
ms.topic: conceptual
helpviewer_keywords: 
  - "viewing logs"
  - "displaying log files"
  - "Setup [SQL Server], logs"
  - "installation log files [SQL Server]"
  - "installing SQL Server, logs"
  - "errors [SQL Server], Setup"
  - "logs [SQL Server], Setup"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# View and Read SQL Server Setup Log Files

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Setup creates log files in a dated and time-stamped folder within **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** by default, where *nnn* are numbers that correspond to the version of SQL that's being installed. The time-stamped log folder name format is YYYYMMDD_hhmmss. When Setup is executed in unattended mode, the logs are created within %temp%\sqlsetup*.log. All files in the log folder are archived into the Log\*.cab file in their respective log folder.  

   | File           | Path |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI Log Files** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **For unattended installations** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > The numbers in the path *nnn* correspond to the version of SQL being installed. In the above picture, SQL 2017 was installed, so the folder is 140. For SQL 2016, the folder would be 130, and for SQL 2014 the folder would be 120.
  
 SQL server setup completes three basic phases: 
  
1.  Global Rules verification: validates basic system requirements
2.  Component update: checks to see if there are any updates available for the media being installed
3.  User-requested action: allows the user to select and customize features
  

This workflow produces a single summary log, and either a single detail log for a base SQL Server installation, or two detail logs for when update, such as a service pack, is installed along with the base installation. 
  
Additionally, there are datastore files that contain a snapshot of the state of all the configuration objects that are being tracked by the setup process, and are useful for troubleshooting configuration errors. XML dump files are created for each execution phase and are saved in the Datastore log subfolder under the time-stamped log folder. 

The following sections describe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup log files.  
  
## Summary.txt file 
  
### Overview  
 This file shows the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that were detected during Setup, the operating system environment, command-line parameter values if they are specified, and the overall status of each MSI/MSP that was executed.
  
 The log is organized into the following sections:
  
-   An overall summary of the execution  
-   Properties and the configuration of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup was run  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] product features previously installed on the computer  
-   Description of the installation version and installation package properties
-   Runtime input settings that are provided during install  
-   Location of the configuration file  
-   Details of the execution results  
-   Global rules  
-   Rules specific to the installation scenario  
-   Failed rules  
-   Location of the rules report file


  >[!NOTE]
  > Note that when patching there can be a number of sub folders (one for each instance being patched, and one for shared features) which contain a similiar set of files (i.e. %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### Location  
 The summary.txt is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 To find errors in the summary text file, search the file by using the "error" or "failed" keywords.
  
## Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### Overview  
 The summary_engine base file is similar to the summary file and is generated during the main workflow.
  
### Location  
 The Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## Detail.txt file
  
### Overview
 Detail.txt is generated for the main workflow such as install or upgrade, and provides the details of the execution. The logs in the file are generated based on the time when each action for the installation was invoked. The text file shows the order in which the actions were executed, as well as their dependencies.  
  
### Location  
 The detail.txt file is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 If an error occurs during the Setup process, the exception or error is logged at the end of this file. To find the errors in this file, first examine the end of the file followed by a search of the file for the "error" or "exception" keywords
    
## MSI log files
  
### Overview  
 The MSI log files provide details of the installation package process. They are generated by the MSIEXEC during the installation of the specified package.  
  
 Types of MSI log files:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### Location  
 The MSI log files are located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 At the end of the file is a summary of the execution, which includes the success or failure status and properties. To find the error in the MSI file, search for "value 3" and review the text before and after.  
  
## ConfigurationFile.ini file
  
### Overview  
 The configuration file contains the input settings that are provided during installation. It can be used to restart the installation without having to enter the settings manually. However, passwords for the accounts, PID, and some parameters are not saved in the configuration file. The settings can be either added to the file or provided by using the command line or the Setup user interface. For more information, see [Install SQL Server 2016 Using a Configuration File](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Location  
 The ConfigurationFile.ini is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm file
  
### Overview  
 The system configuration check report contains a short description for each executed rule, and the execution status.
  
### Location  
The SystemConfigurationCheck_Report.htm is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## See also  
 [Install SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)\`programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmssom: ""
ms.date: "09/09/2016"
ms.prod: sql
ms.reviewer: ""
ms.technology: install
ms.topic: conceptual
helpviewer_keywords: 
  - "viewing logs"
  - "displaying log files"
  - "Setup [SQL Server], logs"
  - "installation log files [SQL Server]"
  - "installing SQL Server, logs"
  - "errors [SQL Server], Setup"
  - "logs [SQL Server], Setup"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# View and Read SQL Server Setup Log Files

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Setup creates log files in a dated and time-stamped folder within **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** by default, where *nnn* are numbers that correspond to the version of SQL that's being installed. The time-stamped log folder name format is YYYYMMDD_hhmmss. When Setup is executed in unattended mode, the logs are created within %temp%\sqlsetup*.log. All files in the log folder are archived into the Log\*.cab file in their respective log folder.  

   | File           | Path |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI Log Files** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **For unattended installations** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > The numbers in the path *nnn* correspond to the version of SQL being installed. In the above picture, SQL 2017 was installed, so the folder is 140. For SQL 2016, the folder would be 130, and for SQL 2014 the folder would be 120.
  
 SQL server setup completes three basic phases: 
  
1.  Global Rules verification: validates basic system requirements
2.  Component update: checks to see if there are any updates available for the media being installed
3.  User-requested action: allows the user to select and customize features
  

This workflow produces a single summary log, and either a single detail log for a base SQL Server installation, or two detail logs for when update, such as a service pack, is installed along with the base installation. 
  
Additionally, there are datastore files that contain a snapshot of the state of all the configuration objects that are being tracked by the setup process, and are useful for troubleshooting configuration errors. XML dump files are created for each execution phase and are saved in the Datastore log subfolder under the time-stamped log folder. 

The following sections describe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup log files.  
  
## Summary.txt file 
  
### Overview  
 This file shows the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components that were detected during Setup, the operating system environment, command-line parameter values if they are specified, and the overall status of each MSI/MSP that was executed.
  
 The log is organized into the following sections:
  
-   An overall summary of the execution  
-   Properties and the configuration of the computer where [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup was run  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] product features previously installed on the computer  
-   Description of the installation version and installation package properties
-   Runtime input settings that are provided during install  
-   Location of the configuration file  
-   Details of the execution results  
-   Global rules  
-   Rules specific to the installation scenario  
-   Failed rules  
-   Location of the rules report file


  >[!NOTE]
  > Note that when patching there can be a number of sub folders (one for each instance being patched, and one for shared features) which contain a similiar set of files (i.e. %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### Location  
 The summary.txt is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 To find errors in the summary text file, search the file by using the "error" or "failed" keywords.
  
## Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### Overview  
 The summary_engine base file is similar to the summary file and is generated during the main workflow.
  
### Location  
 The Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## Detail.txt file
  
### Overview
 Detail.txt is generated for the main workflow such as install or upgrade, and provides the details of the execution. The logs in the file are generated based on the time when each action for the installation was invoked. The text file shows the order in which the actions were executed, as well as their dependencies.  
  
### Location  
 The detail.txt file is located within %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 If an error occurs during the Setup process, the exception or error is logged at the end of this file. To find the errors in this file, first examine the end of the file followed by a search of the file for the "error" or "exception" keywords
    
## MSI log files
  
### Overview  
 The MSI log files provide details of the installation package process. They are generated by the MSIEXEC during the installation of the specified package.  
  
 Types of MSI log files:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### Location  
 The MSI log files are located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 At the end of the file is a summary of the execution, which includes the success or failure status and properties. To find the error in the MSI file, search for "value 3" and review the text before and after.  
  
## ConfigurationFile.ini file
  
### Overview  
 The configuration file contains the input settings that are provided during installation. It can be used to restart the installation without having to enter the settings manually. However, passwords for the accounts, PID, and some parameters are not saved in the configuration file. The settings can be either added to the file or provided by using the command line or the Setup user interface. For more information, see [Install SQL Server 2016 Using a Configuration File](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Location  
 The ConfigurationFile.ini is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm file
  
### Overview  
 The system configuration check report contains a short description for each executed rule, and the execution status.
  
### Location  
The SystemConfigurationCheck_Report.htm is located at %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## See also  
 [Install SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)\`programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmssom: ""
ms.date: "09/09/2016"
ms.prod: sql
ms.reviewer: ""
ms.technology: install
ms.topic: conceptual
helpviewer_keywords: 
  - "viewing logs"
  - "displaying log files"
  - "Setup [SQL Server], logs"
  - "installation log files [SQL Server]"
  - "installing SQL Server, logs"
  - "errors [SQL Server], Setup"
  - "logs [SQL Server], Setup"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
monikerRange: ">=sql-server-2016||=sqlallproducts-allversions"
---
# View and Read SQL Server Setup Log Files

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Setup creates log files in a dated and time-stamped folder within **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** by default, where *nnn* are numbers that correspond to the version of SQL that's being installed. The time-stamped log folder name format is YYYYMMDD_hhmmss. When Setup is executed in unattended mode, the logs are created within %temp%\sqlsetup*.log. All files in the log folder are archived into the Log\*.cab file in their respective log folder.  

   | File           | Path |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI Log Files** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **自動安裝** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > 路徑中的數字 *nnn* 對應至即將安裝的 SQL 版本。 在上圖中，已安裝 SQL 2017，因此資料夾是 140。 如果是 SQL 2016，資料夾會是 130，而 SQL 2014 的資料夾則是 120。
  
 SQL Server 安裝程式會完成三個基本階段： 
  
1.  全域規則驗證：驗證基本系統需求
2.  元件更新：檢查是否有任何更新可用於即將安裝的媒體
3.  使用者要求的動作：可讓使用者選取和自訂功能
  

此工作流程會產生單一摘要記錄檔，以及和基底安裝一起安裝的基底 SQL Server 安裝單一詳細記錄檔 (如 Service Pack)，或更新時為兩個詳細記錄檔。 
  
而且，資料存放區檔案包含安裝程序所追蹤之所有設定物件的狀態快照集，對於針對設定錯誤進行疑難排解很有用。 XML 傾印檔案會針對每個執行階段建立，並且會儲存在資料存放區記錄檔子資料夾的時間戳記記錄檔資料夾下。 

下列各節描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式記錄檔。  
  
## <a name="summarytxt-file"></a>Summary.txt 檔案 
  
### <a name="overview"></a>概觀  
 此檔案會顯示安裝期間偵測到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件、作業系統環境、命令列參數值 (如果有指定)，以及已執行之每個 MSI/MSP 的整體狀態。
  
 記錄檔組織成下列各區段：
  
-   執行的整體摘要  
-   執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式所在電腦的屬性和組態  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 先前安裝在電腦上的產品功能  
-   安裝版本與安裝套件屬性的描述
-   安裝期間提供的執行階段輸入設定  
-   組態檔的位置  
-   執行結果的詳細資料  
-   全域規則  
-   安裝狀況專屬的規則  
-   失敗的規則  
-   規則報表檔案的位置


  >[!NOTE]
  > 請注意，在修補時，可能會有多個子資料夾 (一個用於每個要修補的執行個體，一個用於共用的功能) 包含一組類似的檔案 (亦即 %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER)。 
  
### <a name="location"></a>位置  
 Summary.txt 位在 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\ 內。
  
 若要尋找摘要文字檔中的錯誤，使用 "error" 或 "failed" 等關鍵字搜尋檔案。
  
## <a name="summarymachinenameyyyymmddhhmmsstxt-file"></a>Summary_\<電腦名稱>_YYYYMMDD_HHMMss.txt 檔案
  
### <a name="overview"></a>概觀  
 summary_engine base 檔案與摘要檔案類似，而且是在主要工作流程期間產生的。
  
### <a name="location"></a>位置  
 Summary_\<MachineName>_YYYYMMDD_HHMMss.txt 檔案位於 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\。
  
  
## <a name="detailtxt-file"></a>Detail.txt 檔案
  
### <a name="overview"></a>概觀
 安裝或升級之類的主要工作流程會產生 Detail.txt，並提供執行的詳細資料。 檔案中的記錄是根據叫用每個安裝動作的時間所產生。 此文字檔會顯示動作的執行順序，以及它們的相依性。  
  
### <a name="location"></a>位置  
 Detail.txt 檔案位於 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt。  
  
 如果在安裝程序期間發生錯誤，就會在此檔案的結尾記錄例外狀況或錯誤。 若要尋找此檔案中的錯誤，請先檢查檔案的結尾，然後再搜尋檔案中的 "error" 或 "exception" 等關鍵字
    
## <a name="msi-log-files"></a>MSI 記錄檔
  
### <a name="overview"></a>概觀  
 MSI 記錄檔會提供安裝套件程序的詳細資料。 在指定之套件的安裝期間，MSIEXEC 會產生這些記錄檔。  
  
 MSI 記錄檔的類型：
  
-   \<功能>_\<架構>\_\<互動>.log   
-   \<功能>_\<架構>\_\<語言>\_\<互動>.log   
-   \<功能>_\<架構>\_\<互動>\_\<工作流程>.log  
  
### <a name="location"></a>位置  
 MSI 記錄檔位於 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<名稱\>.log。  
  
 檔案的結尾是執行的摘要，其中包含成功或失敗狀態以及屬性。 若要尋找 MSI 檔案中的錯誤，請搜尋 "value 3"，並檢閱之前和之後的文字。  
  
## <a name="configurationfileini-file"></a>ConfigurationFile.ini 檔案
  
### <a name="overview"></a>概觀  
 組態檔包含安裝期間提供的輸入設定。 該檔案可以用來重新啟動安裝，而不必手動輸入設定。 不過，帳號的密碼、PID 與某些參數不會儲存在組態檔中。 這些設定可以加入至檔案，或者使用命令列或安裝程式使用者介面提供。 如需詳細資訊，請參閱 [使用組態檔安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)。  
  
### <a name="location"></a>位置  
 ConfigurationFile.ini 位於 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\。  
  
## <a name="systemconfigurationcheckreporthtm-file"></a>SystemConfigurationCheck_Report.htm 檔案
  
### <a name="overview"></a>概觀  
 系統組態檢查報告包含每個已執行規則以及執行狀態的簡短描述。
  
### <a name="location"></a>位置  
SystemConfigurationCheck_Report.htm 位於 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\。

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## <a name="see-also"></a>另請參閱  
 [安裝 SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)
