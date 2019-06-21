---
title: 系統需求、安裝和驅動程式檔案 | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9b48188cbc1eb25774bc127246514d82ca5ef475
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66841090"
---
# <a name="system-requirements-installation-and-driver-files"></a>系統需求、安裝和驅動程式檔案
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

適用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC Driver 11 支援連線到 SQL Server 2014、SQL Server 2012、[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] 與 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  
  
Windows 上的 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以安裝在也有一或多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本的電腦上。  
  
ODBC Driver 13 和 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，除此之外，支援 SQL Server 2016。 

ODBC Driver 17 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援上述所有項目，以及 SQL Server 2017。

ODBC Driver 17 for SQL Server 支援 SQL Server 2019 開頭 17.3 版的驅動程式。

您在連接字串中指定的驅動程式名稱是`ODBC Driver 11 for SQL Server`或是`ODBC Driver 13 for SQL Server`（適用於 13 和 13.1） 或`ODBC Driver 17 for SQL Server`。
  
## <a name="supported-operating-systems"></a>支援的作業系統

您可以在下列 Windows 作業系統上以驅動程式執行應用程式：  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(ODBC Driver 11 只)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>安裝 Microsoft ODBC Driver for SQL Server

當您執行安裝的驅動程式`msodbcsql.msi`從下列連結之一：

- [下載 Microsoft ODBC Driver 17 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=56567)
- [下載 Microsoft ODBC Driver 13.1 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [下載 Microsoft ODBC Driver 13 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [下載 Microsoft ODBC Driver 11 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=36434)。 

> [!NOTE]
> 對於使用者而言有驅動程式 17.1.0.1 或以下的安裝，建議，它手動解除安裝，再安裝較新版本的驅動程式

它可以與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 並存安裝。  

當您叫用 `msodbcsql.msi` 時，預設會安裝用戶端元件。 用戶端元件是支援應用程式執行的檔案 (應用程式則是利用驅動程式所開發)。 如果要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=ALL`。 例如：  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 如果您使用 `/passive`、`/qn`、`/qb` 或 `/qr` 選項進行安裝，則指定 `IACCEPTMSODBCSQLLICENSETERMS=YES` 可接受使用者授權條款。 此選項必須以全部大寫的字母指定。 例如：  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 若要進行無訊息解除安裝：  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
當應用程式使用驅動程式時，此應用程式應會透過 `APPGUID` 安裝選項來指出其取決於驅動程式。 這麼做可讓驅動程式安裝程式在解除安裝前，報告相依的應用程式。 若要指定驅動程式的相依性，請在以無訊息模式安裝驅動程式時，將 `APPGUID` 命令列參數設定為您的產品代碼。 (使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。)例如：  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>命令列工具：sqlcmd.exe 和 bcp.exe

`bcp.exe`並`sqlcmd.exe`工具的驅動程式搭配使用，請下載位置[Microsoft Command Line Utilities 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36433)，[適用於 SQL Server 的 Microsoft 命令列公用程式 13](https://www.microsoft.com/download/details.aspx?id=52680)，或[適用於 SQL Server 的 Microsoft 命令列公用程式 13.1](https://www.microsoft.com/download/details.aspx?id=53591)。 驅動程式是安裝的必要條件`sqlcmd.exe`和`bcp.exe`。
  
`bcp.exe` 並`sqlcmd.exe`會安裝在`110\Tools`的子資料夾`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC`版本 11，和`130\Tools`13 和 13.1。

使用 BCP 函式的應用程式必須指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  

比方說，當您編譯的 ODBC 應用程式`msodbcsql11.lib`和`msodbcsql.h`，使用 「 驅動程式 = {ODBC Driver 11 for SQL Server}"的連接字串中。

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上的 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的元件 
 Windows 上的 ODBC 驅動程式包含下列元件：
 
|元件|描述|  
|---------------|-----------------|  
|msodbcsql17.dll 或 <br> msodbcsql13.dll 或 <br> msodbcsql11.dll|動態連結程式庫 (DLL) 檔案，其中包含驅動程式的所有功能。 此檔案會安裝在 %systemroot%\system32 中。|  
|msodbcdiag17.dll 或 <br> msodbcdiag13.dll 或 <br> msodbcdiag11.dll|動態連結程式庫 (DLL) 檔案，其中包含驅動程式的診斷 （追蹤） 介面。 此檔案會安裝在 %systemroot%\system32 中。|
|msodbcsqlr17.rll 或 <br> msodbcsqlr13.rll 或 <br> msodbcsqlr11.rll|隨附驅動程式程式庫的資源檔。 此檔案會安裝在 %systemroot%\system32\1033 中。| 
|s13ch_msodbcsql.chm 或 <br> s11ch_msodbcsql.chm |資料來源精靈說明檔，其中記載如何建立驅動程式的資料來源。 這個檔案會安裝在 %SYSTEMROOT%\System32\1033 <br /> <br /> **注意：** 沒有 ODBC Driver 17 for chm 檔案。 |  
|msodbcsql.h|標頭檔，其中包含使用驅動程式所需的所有新定義。<br /><br /> **注意**  ：您無法在相同的程式中參考 msodbcsql.h 和 odbcss.h。<br /><br /> ODBC Driver 17 或 13 的 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK 中。 <br /> ODBC Driver 11 的 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。| 
|msodbcsql17.lib 或 <br> msodbcsql13.lib 或 <br> msodbcsql11.lib|呼叫 **bcp** 公用程式函式 (屬於驅動程式的一部分) 所需的程式庫檔案。<br /><br /> **注意**：如果您在程式中參考這個程式庫檔，請確定它在您的系統路徑以及使用此應用程式之系統的系統路徑中。<br /><br /> msodbcsql17.lib 或 msodbcsql13.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK 中。<br /> msodbcsql11.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。|

  
## <a name="see-also"></a>另請參閱  
 [Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
