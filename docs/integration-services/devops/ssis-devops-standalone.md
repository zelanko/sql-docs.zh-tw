---
title: 獨立 SQL Server Integration Services (SSIS) DevOps 工具 | Microsoft Docs
description: 了解如何使用獨立 SSIS DevOps 工具建置 SSIS CICD。
ms.date: 10/16/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 52578422cc9f68c728c901cf39bf05425576133b
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521092"
---
# <a name="standalone-sql-server-integration-service-ssis-devops-tools-preview"></a>獨立 SQL Server Integration Services (SSIS) DevOps 工具 (預覽)

獨立 **SSIS DevOps 工具** 可為使用者提供一組可執行檔以執行 SSIS CICD 工作。 由於這些可執行檔對 Visual Studio 或 SSIS 執行階段的安裝並沒有任何相依性，因此可以輕鬆地與任何 CICD 平台整合。 所提供的可執行檔為：

- SSISBuild.exe：在專案部署模型或套件部署模型中建置 SSIS 專案。
- SSISDeploy.exe：將 ISPAC 檔案部署到 SSIS 目錄，或是將 DTSX 檔案及其相依性部署到檔案系統。

## <a name="installation"></a>安裝

需要 .NET Framework 4.6.2 或更高版本。

請從[下載中心](https://aka.ms/AA9xp65) \(英文\) 下載最新的安裝程式，然後透過精靈或命令列安裝：

- 透過精靈安裝

按兩下 .exe 檔案以安裝，然後指定要將可執行檔和相依性檔案解壓縮的目標資料夾。

![安裝位置](media/installation-location.png)

- 透過命令列安裝

```
SSISDevOpsTools.exe /Q /C /T:<full path>
```

![安裝命令列](media/installation-command-line.png)


## <a name="ssisbuildexe"></a>SSISBuild.exe

**語法**

```
SSISBuild.exe -project|-p:<dtproj file path> [-configuration|-c:<configuration name>] [-projectPassword|-pp:<project password>] [-stripSensitive|-ss] [-output|-o:<output path>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**參數**

|參數|描述|
|---------|---------|
|-project \|-p:\<dtproj file path>|要建置之 dtproj 檔案的檔案路徑。|
|-configuration\|-c:\<configuration name>|要用於建置的專案組態名稱。 如果未提供，則會預設為 dtproj 檔案中第一個定義的專案組態。|
|-projectPassword\|-pp:\<project password>|SSIS 專案及其套件的密碼。 只有在 SSIS 專案及套件的保護層級為 EncryptSensitiveWithPassword 或 EncryptAllWithPassword 時，此引數才會有效。 針對套件部署模型，所有套件都必須共用由此引數所指定的相同密碼。|
|-stripSensitive\|-ss|將 SSIS 專案的保護層級轉換成 DontSaveSensitve。 當保護層級為 EncryptSensitiveWithPassword 或 EncryptAllWithPassword 時，必須正確設定 -projectPassword 引數。 此選項僅適用於專案部署模型。|
|-output\|-o:\<output path>|組建成品的輸出路徑。 此引數的值將會覆寫專案組態中的預設輸出路徑。|
|-log\|-l:\<log level>[;\<log path>]|與記錄相關的設定。 <li>記錄層級：系統只會將具有相等或更高記錄層級的記錄寫入記錄檔。 有四個記錄層級 (從低到高)：DIAG、INFO、WRN、ERR。 如果未指定記錄層級，預設的記錄層級是 INFO。 <li> 記錄路徑：保存記錄之檔案的路徑。 如果未指定路徑，將不會產生記錄檔。|
|-quiet\|-q|不要在標準輸出中顯示任何記錄。|
|-help\|-h\|-?|顯示此命令列公用程式的詳細使用方式資訊。|

**範例**

- 使用第一個定義的專案組態建置 dtproj，且不使用密碼加密：    
    ```
    SSISBuild.exe -p:"C:\projects\demo\demo.dtproj"
    ```

- 使用 "DevConfiguration" 組態建置 dtproj、使用密碼加密，以及將組建成品輸出到特定資料夾：
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -o:D:\folder
    ```

- 使用 "DevConfiguration" 組態建置 dtproj、使用密碼加密、分割其敏感性資料，以及使用 DIAG 記錄層級：
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -ss -l:diag
    ```

## <a name="ssisdeployexe"></a>SSISDeploy.exe

**語法**

```
SSISDeploy.exe -source|-s:<source path> -destination|-d:<type>;<path>[;server] [-authType|-at:<auth type name>] [-connectionStringSuffix|-css:<connection string suffix>] [-projectPassword|-pp:<project password>] [-username|-u:<username>] [-password|-p:<password>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**參數**

|參數|描述|
|---------|---------|
|-source\|-s:\<source path>|要部署之成品的本機檔案路徑。 允許 ISPAC、DTSX、DTSX 之資料夾的路徑、SSISDeploymentManfiest。|
|-destination\|-d:\<type>;\<path>[;server]|要將來源檔案部署到的目的地類型、目的地資料夾的路徑，以及 SSIS 目錄的伺服器名稱。 目前我們支援下列兩種目的地類型： <li> *CATALOG*：將單一或多個 ISPAC 檔案部署到指定的 SSIS 目錄。 CATALOG 目的地的路徑應該要採用下列格式： <br> /SSISDB/\<folder name>[/\<project name>] <br> 選擇性的 <project name> 僅在來源指定單一 ISPAC 檔案路徑時才有效。 針對 CATALOG 目的地必須指定伺服器名稱。 <li> *FILE*：將在單一或多個 SSISDeploymentManifest 檔案中指定的 SSIS 套件或檔案部署到指定的檔案系統路徑。 FILE 目的地的路徑可以是本機資料夾路徑或網路資料夾路徑，其格式如下： <br>\\\\\<machine name>\\\<folder name>[\\\<sub folder name>\...]|
|-authType\|-at:\<auth type name>|存取 SQL Server 的驗證類型。 此為 CATALOG 目的地的必要項目。 支援下列類型： <li> WIN：Windows 驗證 <li> SQL：SQL Server 驗證 <li> ADPWD：Active Directory - 密碼 <li> ADINT：Active Directory - 整合式|
|-connectionStringSuffix\|-css:\<connection string suffix> |連接字串的尾碼，其用來連線到 SSIS 目錄。|
|-projectPassword\|-pp:\<project password> |將 ISPAC 或 DTSX 檔案解密的密碼。|
|-username\|-u:\<username>  |存取指定 SSIS 目錄或檔案系統的使用者名稱。 針對檔案系統存取，允許使用網域名稱作為前置詞。|
|-password\|-p:\<password>  |存取指定 SSIS 目錄或檔案系統的密碼。|
|-log\|-l:\<log level>[;\<log path>] |執行此公用程式的記錄相關設定。 <li> 記錄層級：系統只會將具有相等或更高記錄層級的記錄寫入記錄檔。 有四個記錄層級 (從低到高)：DIAG、INFO、WRN、ERR。 如果未指定記錄層級，預設的記錄層級是 INFO。 <li> 記錄路徑：保存記錄之檔案的路徑。 如果未指定路徑，將不會產生記錄檔。|
|-quiet\|-q |不要在標準輸出中顯示記錄。|
|-help\|-h\|-?  |顯示此命令列公用程式的詳細使用方式資訊。|

**範例**

- 將未使用密碼加密的單一 ISPAC 部署到具有 Windows 驗證的 SSIS 目錄。
    ```
    SSISDeploy.exe -s:D:\myfolder\demo.ispac -d:catalog;/SSISDB/destfolder;myssisserver -at:win
    ```

- 將使用密碼加密的單一 ISPAC 部署到具有 SQL 驗證的 SSIS 目錄，並將專案重新命名。
    ```
    SSISDeploy.exe -s:D:\myfolder\test.ispac -d:catalog;/SSISDB/folder/testproj;myssisserver -at:sql -u:sqlusername -p:sqlpassword -pp:encryptionpassword
    ```

- 將單一 SSISDeploymentManifest 及其相關聯的檔案部署到 Azure 檔案共用。
    ```
    SSISDeploy.exe -s:D:\myfolder\mypackage.SSISDeploymentManifest -d:file;\\myssisshare.file.core.windows.net\destfolder -u:Azure\myssisshare -p:storagekey
    ```

- 將包含 DTSX 檔案的資料夾部署到內部部署檔案系統。
    ```
    SSISDeploy.exe -s:D:\myfolder -d:file;\\myssisshare\destfolder
    ```

## <a name="release-notes"></a>版本資訊

### <a name="version-011-preview"></a>0\.1.1 版預覽

發行日期：2020 年 11 月 11 日

- 已修正將 ispac 部署至 SSIS 目錄時，SSISDeploy.exe 無法載入組件的問題。

### <a name="version-010-preview"></a>0\.1.0 版預覽

發行日期：2020 年 10 月 16 日

獨立 SSIS DevOps 工具的初始預覽版本。

## <a name="next-steps"></a>後續步驟

- 取得[獨立 SSIS DevOps 工具](https://aka.ms/AA9xp65) \(英文\)
- 如有任何疑問，請瀏覽[問與答](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools&ssr=false#qna) \(英文\)
