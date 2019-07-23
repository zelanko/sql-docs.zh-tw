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
ms.openlocfilehash: 76016e87767f4efbca9a6c845af6464ab3ca26ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989406"
---
# <a name="system-requirements-installation-and-driver-files"></a>系統需求、安裝和驅動程式檔案
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

適用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC Driver 11 支援連線到 SQL Server 2014、SQL Server 2012、[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] 與 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  
  
Windows 上的 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以安裝在也有一或多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本的電腦上。  
  
除了上述以外, ODBC Driver 13 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]和13.1 支援 SQL Server 2016。 

ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援上述所有版本, 而且也 SQL Server 2017。

ODBC Driver 17 for SQL Server 支援從驅動程式版本17.3 開始 SQL Server 2019。

您在連接字串中指定的驅動程式名稱是`ODBC Driver 11 for SQL Server`或`ODBC Driver 13 for SQL Server` (適用于13和 13.1) 或`ODBC Driver 17 for SQL Server`。
  
## <a name="supported-operating-systems"></a>支援的作業系統

您可以在下列 Windows 作業系統上以驅動程式執行應用程式：  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(僅限 ODBC Driver 11)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>安裝 Microsoft ODBC Driver for SQL Server

當您從下列其中一個連結`msodbcsql.msi`執行時, 會安裝驅動程式:

- [下載 Microsoft ODBC Driver 17 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=56567)
- [下載 Microsoft ODBC Driver 13.1 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [下載 Microsoft ODBC Driver 13 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [下載 Microsoft ODBC Driver 11 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=36434)。 

> [!NOTE]
> 針對已安裝驅動程式17.1.0.1 或更新版本的使用者, 建議您先手動卸載, 再安裝新版的驅動程式。

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

與`bcp.exe`驅動`sqlcmd.exe`程式搭配使用的和工具, 可以在[microsoft 命令列公用程式 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36433)、 [microsoft 命令列公用程式 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)或[microsoft 命令列公用程式13.1 下載SQL Server](https://www.microsoft.com/download/details.aspx?id=53591)。 驅動程式是安裝`sqlcmd.exe`和`bcp.exe`的必要條件。
  
`bcp.exe`和`sqlcmd.exe`會安裝`110\Tools`在第11版`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC`的子資料夾中, `130\Tools`以及13和13.1。

使用 BCP 函式的應用程式必須指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  

例如, 當您使用`msodbcsql11.lib`和`msodbcsql.h`編譯 ODBC 應用程式時, 請在連接字串中使用 "DRIVER = {ODBC DRIVER 11 for SQL Server}"。

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上的 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的元件 
 Windows 上的 ODBC 驅動程式包含下列元件：
 
|元件|Description|  
|---------------|-----------------|  
|msodbcsql17.dll 或 <br> msodbcsql13.dll 或 <br> msodbcsql11.dll|動態連結程式庫 (DLL) 檔案，其中包含驅動程式的所有功能。 此檔案會安裝在%Systemroot%\system32 中。中|  
|msodbcdiag17 或 <br> msodbcdiag13 或 <br> msodbcdiag11.dll|包含驅動程式診斷 (追蹤) 介面的動態連結程式庫 (DLL) 檔案。 此檔案會安裝在%Systemroot%\system32 中。中|
|msodbcsqlr17.rll 或 <br> msodbcsqlr13.rll 或 <br> msodbcsqlr11.rll|隨附驅動程式程式庫的資源檔。 此檔案會安裝在%Systemroot%\system32\1033 中。中| 
|s13ch_msodbcsql.chm 或 <br> s11ch_msodbcsql.chm |資料來源精靈說明檔，其中記載如何建立驅動程式的資料來源。 此檔案會安裝在%Systemroot%\system32\1033 中中 <br /> <br /> **注意:** 沒有 ODBC 驅動程式17的 chm 檔案。 |  
|msodbcsql.h|標頭檔，其中包含使用驅動程式所需的所有新定義。<br /><br /> **注意**  ：您無法在相同的程式中參考 msodbcsql.h 和 odbcss.h。<br /><br /> ODBC Driver 17 或 13 的 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK 中。 <br /> ODBC Driver 11 的 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。| 
|msodbcsql17.lib 或 <br> msodbcsql13.lib 或 <br> msodbcsql11.lib|呼叫 **bcp** 公用程式函式 (屬於驅動程式的一部分) 所需的程式庫檔案。<br /><br /> **注意**：如果您在程式中參考這個程式庫檔，請確定它在您的系統路徑以及使用此應用程式之系統的系統路徑中。<br /><br /> msodbcsql17.lib 或 msodbcsql13.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK 中。<br /> msodbcsql11.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。|

  
## <a name="see-also"></a>另請參閱  
 [Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
