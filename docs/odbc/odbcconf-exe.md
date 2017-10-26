---
title: "ODBCCONF。EXE |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db8ff09a2b77f51c97ab73d6d994e1e1b4dce2a1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbcconfexe"></a>ODBCCONF。EXE
ODBCCONF.exe 是命令列工具，可讓您設定 ODBC 驅動程式和資料來源的名稱。  
  
> [!NOTE]  
>  Windows Data Access Components 的未來版本將移除 ODBCCONF.exe。 避免使用這項功能，並規劃修改目前使用這項功能的應用程式。 您可以使用 PowerShell 命令來管理驅動程式和資料來源。 如需下列 PowerShell 命令的詳細資訊，請參閱[Windows Data Access Components cmdlet](https://technet.microsoft.com/library/hh771019.aspx)。  
  
## <a name="syntax"></a>語法  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>引數  
 *參數*  
 零或多個參數的選項。 如需可用的參數清單，請參閱 < 備註 > 一節，本主題稍後的。  
  
 *動作*  
 一個要執行的動作。 如需可用選項的清單，請參閱 < 備註 > 一節。  
  
## <a name="remarks"></a>備註  
 可使用下列參數：  
  
|參數|Description|  
|------------|-----------------|  
|/ A {*動作*}|指定的動作。<br /><br /> 如果只指定一個動作/A 是選擇性的。|  
|/?|顯示 ODBCCONF 使用量。EXE。|  
|/C|如果動作便會失敗，繼續進行處理。|  
|/E|清除指定與 /F，當處理完成時的回應檔案。|  
|/F|使用回應檔案，例如`odbcconf /F my.rsp`。<br /><br /> my.rsp 可能看起來像這樣：`REGSVR c:\my.dll`<br /><br /> / A 不使用回應檔案中。|  
|/H|顯示使用方式 （說明）。 這個參數是相同 /？。|  
|/ L [*模式*]*檔名*|程式輸出傳送到的檔案中的三個模式的其中一個： 標準 (n)、 詳細資訊 (v) 和 偵錯 (d)。 偵錯模式記錄由 odbcconf.exe 載入的 Dll。<br /><br /> 如果您指定 /L 但不模式時，記錄檔將會是空白。<br /><br /> 例如， **/Lv.log.txt**。|  
|/R|在重新開機後，就會執行的動作。|  
|/S|無訊息模式。 不會顯示錯誤訊息。|  
  
 可用的下列動作：  
  
|動作|Description|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name**驅動程式專屬的組態參數*|會載入適當的驅動程式安裝 DLL 呼叫**ConfigDriver**函式。<br /><br /> 相當於[SQLConfigDriver 函式](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGDRIVER [驅動程式名稱]"CPTimeout = 60"}<br /><br /> / A {CONFIGDRIVER [驅動程式名稱]"DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*名稱*&#124;*屬性*|加入或修改系統資料來源。<br /><br /> 相當於[SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGDSN < SQL Server >"DSN = 名稱 &#124;Server = srv"}|  
|CONFIGSYSDSN *driver_name* DSN =*名稱*&#124;*屬性*|加入或修改系統資料來源。<br /><br /> 相當於[SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGSYSDSN < SQL Server >"DSN = 名稱 &#124;Server = srv"}|  
|INSTALLDRIVER|相當於[SQLInstallDriverEx 函式](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 傳遞至 INSTALLDRIVER 關鍵字-值配對語法的詳細資訊，請參閱[驅動程式規格子機碼](../odbc/reference/install/driver-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> / A {INSTALLDRIVER"您的驅動程式 &#124;Driver=c:\your.dll &#124;Setup=c:\your.dll &#124;APILevel = 2 &#124;ConnectFunctions = YYY &#124;DriverODBCVer = 03.50 &#124;FileUsage = 0 &#124;SQLLevel = 1"}|  
|INSTALLTRANSLATOR*轉譯器設定**驅動程式路徑*|將轉譯程式，以相關資訊加入**HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST。INI\ODBC 轉譯器**登錄機碼。<br /><br /> 相當於[SQLInstallTranslatorEx 函式](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 傳遞至 INSTALLDRIVER 關鍵字-值配對語法的詳細資訊，請參閱[轉譯器規格子機碼](../odbc/reference/install/translator-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> / A {INSTALLTRANSLATOR 「 我的轉譯程式 &#124;Translator=c:\my.dll &#124;Setup=c:\my.dll"}|  
|REGSVR *dll*|註冊 DLL。<br /><br /> 相當於 regsvr32.exe。<br /><br /> 例如：<br /><br /> {REGSVR c:\my.dll} / A|  
|SETFILEDSNDIR|當 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC。INI\ODBC 檔案 DSN\DefaultDSNDir 不存在，SETFILEDSNDIR 動作會建立它並將它指派 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir，加上 \ODBC\Data 來源處的值。<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 處的值。INI\ODBC 檔案 DSN\DefaultDSNDir 指定建立的檔案為基礎的資料來源時使用的 ODBC 資料來源管理員 」 中的預設位置。<br /><br /> 例如：<br /><br /> {SETFILEDSNDIR} / A|  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 開啟資料庫連接 (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)

