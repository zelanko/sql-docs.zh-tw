---
title: 系統需求、 安裝和驅動程式檔案 |Microsoft 文件
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1837964d0c0c7736890dd8e73d4e04ced90cda8a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements-installation-and-driver-files"></a>系統需求、安裝和驅動程式檔案
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 支援連接到 SQL Server 2014、SQL Server 2012 R2、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro_md.md)]、 [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]和 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]。  
  
Windows 上的 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 可以安裝在也有一或多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client 版本的電腦上。  
  
ODBC Driver 13 和 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，除了上述項目，支援 SQL Server 2016。 

ODBC 驅動程式為 17[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支援上述所有項目以及 SQL Server 2017。
  
您在連接字串中指定的驅動程式名稱是`ODBC Driver 11 for SQL Server`或`ODBC Driver 13 for SQL Server`（針對 13 和 13.1） 或`ODBC Driver 17 for SQL Server`。
  
## <a name="supported-operating-systems"></a>支援的作業系統

您可以在下列 Windows 作業系統上的驅動程式執行應用程式：  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(ODBC Driver 11 只)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>安裝 Microsoft ODBC Driver for SQL Server

當您執行安裝的驅動程式`msodbcsql.msi`從下列連結：

- [下載 Windows 上的 SQL Server 的 Microsoft ODBC Driver 17](https://www.microsoft.com/download/details.aspx?id=56567)
- [下載 Microsoft ODBC Driver 13.1 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [下載 Microsoft ODBC Driver 13 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [下載 Microsoft ODBC Driver 11 for SQL Server on Windows](https://www.microsoft.com/download/details.aspx?id=36434)。 

它可以是已安裝的並行與[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]原生用戶端。  

當您叫用`msodbcsql.msi`，預設會安裝用戶端元件。 用戶端元件是支援執行使用驅動程式所開發的應用程式的檔案。 若要安裝 SDK 元件，請指定`ADDLOCAL=ALL`命令列上。 例如：  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 指定`IACCEPTMSODBCSQLLICENSETERMS=YES`接受使用者授權條款，如果您使用`/passive`， `/qn`， `/qb`，或`/qr`安裝選項。 此選項必須以全部大寫的字母指定。 例如：  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 若要進行無訊息解除安裝：  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
當應用程式使用驅動程式時，應用程式應該來指出其取決於驅動程式安裝選項透過`APPGUID`。 如此可讓報表相依的應用程式的驅動程式安裝程式，然後再解除安裝。 若要指定相依於驅動程式，設定`APPGUID`您產品的程式碼時以無訊息方式安裝驅動程式的命令列參數。 (使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。)例如：  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>命令列工具： sqlcmd.exe 和 bcp.exe

`bcp.exe`和`sqlcmd.exe`工具的驅動程式搭配使用的下載網址[Microsoft Command Line Utilities 11 for SQL Server](http://www.microsoft.com/download/details.aspx?id=36433)， [Microsoft 命令列公用程式 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)，或[Microsoft Command Line Utilities 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53591)。 驅動程式已安裝的先決條件`sqlcmd.exe`和`bcp.exe`。
  
`bcp.exe` 和`sqlcmd.exe`安裝在`110\Tools`的子資料夾`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC`版本 11，和`130\Tools`13 和 13.1。

使用 BCP 函數的應用程式必須指定相同的版本中隨附的驅動程式之標頭檔與用來編譯應用程式的程式庫。  

例如，當您編譯 ODBC 應用程式與`msodbcsql11.lib`和`msodbcsql.h`，使用 「 驅動程式 = {ODBC Driver 11 for SQL Server}"連接字串中。

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>元件的 Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上 
 Windows 上的 ODBC 驅動程式包含下列元件：
 
|元件|Description|  
|---------------|-----------------|  
|msodbcsql17.dll 或 <br> msodbcsql13.dll 或 <br> msodbcsql11.dll|動態連結程式庫 (DLL) 檔案，其中包含驅動程式的所有功能。 這個檔案會安裝在 %systemroot%\system32。|  
|msodbcdiag17.dll 或 <br> msodbcdiag13.dll 或 <br> msodbcdiag11.dll|動態連結程式庫 (DLL) 檔案包含驅動程式的診斷 （追蹤） 介面。 這個檔案會安裝在 %systemroot%\system32。|
|msodbcsqlr17.rll 或 <br> msodbcsqlr13.rll 或 <br> msodbcsqlr11.rll|隨附驅動程式程式庫的資源檔。 這個檔案會安裝在 %systemroot%\system32\1033。| 
|s13ch_msodbcsql.chm 或 <br> s11ch_msodbcsql.chm |如何建立資料來源驅動程式的文件資料來源精靈說明檔。 這個檔案會安裝在 %SYSTEMROOT%\System32\1033 中 <br /> <br /> **注意：**沒有 ODBC 驅動程式 17 chm 檔案。 |  
|msodbcsql.h|包含新的定義，使用驅動程式所需的所有標頭檔。<br /><br /> **注意**  ：您無法在相同的程式中參考 msodbcsql.h 和 odbcss.h。<br /><br /> ODBC 驅動程式 17 或 13 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK。 <br /> ODBC Driver 11 msodbcsql.h 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client sdk\odbc\110\sdk。| 
|msodbcsql17.lib or <br> msodbcsql13.lib or <br> msodbcsql11.lib|呼叫所需的程式庫檔案**bcp**驅動程式一部分的公用程式函式。<br /><br /> **注意：**如果您在程式中參考此程式庫檔案，請確定它是您的系統路徑以及使用應用程式的系統路徑中。<br /><br /> msodbcsql17.lib 或 msodbcsql13.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK。<br /> msodbcsql11.lib 會安裝在 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK 中。|

  
## <a name="see-also"></a>另請參閱  
 [Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
