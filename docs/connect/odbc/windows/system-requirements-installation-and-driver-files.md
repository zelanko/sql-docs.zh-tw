---
title: 系統需求、安裝和驅動程式檔案 | Microsoft Docs
description: 此文章說明 Microsoft ODBC Driver for SQL Server 的系統需求。
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f0ce55639f5d6835c50744114a48d510d41c887
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930349"
---
# <a name="system-requirements-installation-and-driver-files"></a>系統需求、安裝和驅動程式檔案

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

此文章會討論連線到 SQL Server 的 ODBC 驅動程式。

## <a name="sql-version-compatibility"></a>SQL 的版本相容性

相容性指出驅動程式已針對驅動程式發行時的現有 SQL 版本進行相容性測試。 SQL Server 版本通常會嘗試維持與現有用戶端驅動程式的回溯相容性。 但 SQL Server 版本的新功能可能無法與舊版用戶端驅動程式搭配使用。

|資料庫版本&nbsp;&#8594;<br />&#8595; 驅動程式版本|Azure SQL Database|Azure Synapse Analytics|Azure SQL 受控執行個體|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|SQL Server 2008 R2|SQL Server 2008|SQL Server 2005|
|----|---|---|---|---|---|---|---|---|---|---|---|
|17.6|是|是|是|是|是|是|是|是|   |   |   |
|17.5|是|是|是|是|是|是|是|是|   |   |   |
|17.4|是|是|是|是|是|是|是|是|   |   |   |
|17.3|是|是|是|是|是|是|是|是|是|是|   |
|17.2|是|是|是|   |是|是|是|是|是|是|   |
|17.1|是|是|是|   |是|是|是|是|是|是|   |
|17.0|是|是|是|   |是|是|是|是|是|是|   |
|13.1|   |   |   |   |是|是|是|是|是|是|   |
|13  |   |   |   |   |   |是|是|是|是|是|   |
|11  |   |   |   |   |   |   |是|是|是|是|是|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>連接字串詳細資料

您在連接字串中指定的驅動程式名稱是 `ODBC Driver 11 for SQL Server`、`ODBC Driver 13 for SQL Server` (同時適用於 13 與 13.1) 或 `ODBC Driver 17 for SQL Server`。

## <a name="supported-operating-systems"></a>支援的作業系統

下表指出不同 Windows 作業系統版本的驅動程式版本支援：

|作業系統&nbsp;&#8594;<br />&#8595; 驅動程式版本|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|Windows Server 2012|Windows Server 2008 R2|Windows 10|Windows 8.1|Windows 7|Windows Vista SP2|
|----|---|---|---|---|---|---|---|---|---|
|17.6|是|是|是|是|   |是|是|   |   |
|17.5|是|是|是|是|   |是|是|   |   |
|17.4|是|是|是|是|是|是|是|是|   |
|17.3|是|是|是|是|是|是|是|是|   |
|17.2|   |是|是|是|是|是|是|是|   |
|17.1|   |是|是|是|是|是|是|是|   |
|17.0|   |是|是|是|是|是|是|是|   |
|13.1|   |是|是|是|是|是|是|是|   |
|13  |   |   |   |是|是|   |是|是|   |
|11  |   |   |   |是|是|   |   |是|是|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>安裝 Microsoft ODBC Driver for SQL Server

當從[下載 Windows 版](../download-odbc-driver-for-sql-server.md#download-for-windows)中的其中一個連結執行 `msodbcsql.msi` 時，就會安裝驅動程式。

> [!NOTE]
> 針對已安裝驅動程式 17.1.0.1 或更新版本的使用者，建議您先手動將其解除安裝，再安裝較新版本的驅動程式。

### <a name="side-by-side-with-native-client"></a>與 Native Client 並存安裝

驅動程式可以與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 並存安裝。 驅動程式的主要版本 (11、13、17) 也可以彼此並存安裝。

當您叫用 `msodbcsql.msi` 時，預設會安裝用戶端元件。 用戶端元件是支援應用程式執行的檔案 (應用程式則是利用驅動程式所開發)。 如果要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=ALL`。 範例如下。
  
```console
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  

### <a name="end-user-license"></a>終端使用者授權

如果您使用 `/passive`、`/qn`、`/qb` 或 `/qr` 選項進行安裝，則指定 `IACCEPTMSODBCSQLLICENSETERMS=YES` 可接受使用者授權條款。 此選項必須以全部大寫的字母指定。 範例如下。
  
```console
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  

### <a name="silent-uninstall"></a>無訊息解除安裝

下列範例示範如何執行無訊息解除安裝。
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>指出相依性

當應用程式使用驅動程式時，此應用程式應會透過 `APPGUID` 安裝選項來指出其取決於驅動程式。 這樣可讓驅動程式安裝程式在解除安裝前，報告相依的應用程式。 若要指定驅動程式的相依性，請在以無訊息模式安裝驅動程式時，將 `APPGUID` 命令列參數設定為您的產品代碼。 使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。 範例如下。
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>命令列工具：sqlcmd.exe 和 bcp.exe

適用與驅動程式搭配使用的 `bcp.exe` 和 `sqlcmd.exe` 工具，可以在[適用於 SQL Server 的 Microsoft 命令列公用程式 11](https://www.microsoft.com/download/details.aspx?id=36433)、[適用於 SQL Server 的 Microsoft 命令列公用程式 13](https://www.microsoft.com/download/details.aspx?id=52680) 或[適用於 SQL Server 的 Microsoft 命令列公用程式 13.1](https://www.microsoft.com/download/details.aspx?id=53591) 下載。 驅動程式是安裝 `sqlcmd.exe` 與 `bcp.exe` 的先決條件。
  
`bcp.exe` 與 `sqlcmd.exe` 安裝在 11 版 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` 的 `110\Tools` 子資料夾中，與 13 與 13.1 版的 `130\Tools` 子資料夾中。

使用 BCP 函式的應用程式必須指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  

例如，當您編譯具有 `msodbcsql11.lib` 與 `msodbcsql.h` 的 ODBC 應用程式時，請在連接字串中使用 "DRIVER={ODBC Driver 11 for SQL Server}"。

## <a name="components-of-the-microsoft-odbc-driver-for-ssnoversion-on-windows"></a>Windows 上的 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的元件

Windows 上的 ODBC 驅動程式包含下列元件：

| 元件 | 描述 |
| :-------- | :---------- |
|msodbcsql17.dll 或 <br/> msodbcsql13.dll 或 <br/> msodbcsql11.dll|動態連結程式庫 (DLL) 檔案，其中包含驅動程式的所有功能。 此檔案會安裝在 %SYSTEMROOT%\System32 中。|  
|msodbcdiag.17 或 <br/> msodbcdiag.13 或 <br/> msodbcdiag11.dll|包含驅動程式診斷 (追蹤) 介面的動態連結程式庫 (DLL) 檔案。 此檔案會安裝在 %SYSTEMROOT%\System32 中。|
|msodbcsqlr17.rll 或 <br/> msodbcsqlr13.rll 或 <br/> msodbcsqlr11.rll|隨附驅動程式程式庫的資源檔。 此檔案會安裝在 %SYSTEMROOT%\System32\1033 中。| 
|s13ch_msodbcsql.chm 或 <br/> s11ch_msodbcsql.chm |資料來源精靈說明檔，其中記載如何建立驅動程式的資料來源。 此檔案會安裝在 %SYSTEMROOT%\System32\1033 中 <br /> <br /> **注意：** 沒有 ODBC Driver 17 的 chm 檔案。 |  
|msodbcsql.h|標頭檔，其中包含使用驅動程式所需的所有新定義。<br /><br /> **注意：** 您無法在相同的程式中參考 msodbcsql.h 與 odbcss.h。<br /><br /> ODBC Driver 17 或 13 的 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK 中。 <br /> ODBC Driver 11 的 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。| 
|msodbcsql17.lib 或 <br/> msodbcsql13.lib 或 <br/> msodbcsql11.lib|呼叫 **bcp** 公用程式函式 (屬於驅動程式的一部分) 所需的程式庫檔案。<br /><br /> **注意：** 如果您在程式中參考這個程式庫檔案，請確定其在您的系統路徑以及使用此應用程式之系統的系統路徑中。<br /><br /> msodbcsql17.lib 或 msodbcsql13.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK 中。<br /> msodbcsql11.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱

[Windows 上的 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
