---
title: ODBCCONF.EXE |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b70622ea038b61883ce7a5307a558a5667139fb1
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491969"
---
# <a name="odbcconfexe"></a>ODBCCONF.CONVERT.EXE
ODBCCONF 是一種命令列工具，可讓您設定 ODBC 驅動程式和資料來源名稱。  
  
> [!NOTE]  
>  ODBCCONF 將會在未來的 Windows Data Access 元件版本中移除。 請避免使用這項功能，並規劃修改目前使用這項功能的應用程式。 您可以使用 PowerShell 命令來管理驅動程式和資料來源。 如需這些 PowerShell 命令的詳細資訊，請參閱[Windows Data Access Components Cmdlet](/powershell/module/wdac)。  
  
## <a name="syntax"></a>語法  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>引數  
 *參數*  
 零或多個參數選項。 如需可用參數的清單，請參閱本主題稍後的「備註」一節。  
  
 *即席*  
 要執行的一個動作。 如需可用選項的清單，請參閱備註一節。  
  
## <a name="remarks"></a>備註  
 可用的參數如下：  
  
|參數|描述|  
|------------|-----------------|  
|/A {*action*}|指定動作。<br /><br /> 如果只指定一個動作，則/a 是選擇性的。|  
|/?|顯示 ODBCCONF 的使用方式。CONVERT.EXE.|  
|/C|如果動作失敗，則會繼續處理。|  
|/E|當處理完成時，清除以/F 指定的回應檔案。|  
|/F|使用回應檔，例如`odbcconf /F my.rsp`。<br /><br /> 我的 .rsp 看起來可能像這樣：`REGSVR c:\my.dll`<br /><br /> /A 不會在回應檔中使用。|  
|/H|顯示使用方式（說明）。 這個參數與/？相同。|  
|/L [*mode*] *filename*|以下列三種模式之一將程式輸出傳送至檔案：一般（n）、詳細資訊（v）和 debug （d）。 [偵錯工具] 模式會記錄 odbcconf 載入的 Dll。<br /><br /> 如果您指定/L 而不使用模式，記錄檔將會是空的。<br /><br /> 例如， **/Lv log .txt**。|  
|/R|動作會在重新開機之後執行。|  
|/S|無訊息模式。 不要顯示錯誤訊息。|  
  
 下列是可用的動作：  
  
|動作|描述|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * 驅動程式特定的設定參數*|載入適當的驅動程式安裝 DLL，並呼叫**ConfigDriver**函式。<br /><br /> 相當於[SQLConfigDriver 函數](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGDRIVER "驅動程式名稱" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "驅動程式名稱" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*name* &#124;*屬性*|加入或修改系統資料來源。<br /><br /> 相當於[SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|CONFIGSYSDSN *driver_name* DSN =*name* &#124;*屬性*|加入或修改系統資料來源。<br /><br /> 相當於[SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|INSTALLDRIVER|相當於[SQLInstallDriverEx 函數](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 如需傳遞至 INSTALLDRIVER 之關鍵字-值組語法的相關資訊，請參閱[驅動程式規格](../odbc/reference/install/driver-specification-subkeys.md)子機碼。<br /><br /> 例如：<br /><br /> /A {INSTALLDRIVER "您的驅動程式 &#124; 驅動程式 = c:\your.dll &#124; 安裝程式 = c:\your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}|  
|INSTALLTRANSLATOR *translator configuration * * 驅動程式路徑*|將翻譯工具的相關資訊新增至**HKEY_LOCAL_MACHINE \software\odbc\odbcinst。INI\ODBC 轉譯**登錄機碼。<br /><br /> 相當於[SQLInstallTranslatorEx 函數](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 如需傳遞至 INSTALLDRIVER 之關鍵字-值組語法的詳細資訊，請參閱[Translator 規格](../odbc/reference/install/translator-specification-subkeys.md)子機碼。<br /><br /> 例如：<br /><br /> /A {INSTALLTRANSLATOR "我的 Translator &#124; Translator = c:\my.dll &#124; Setup = c:\my.dll"}|  
|REGSVR *dll*|註冊 DLL。<br /><br /> 相當於 regsvr32。<br /><br /> 例如：<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|當 HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBC. 時INI\ODBC 檔案 DSN\DefaultDSNDir 不存在，SETFILEDSNDIR 動作會建立該檔案，並為其指派位於 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir 的值，並附加 \ODBC\Data 來源。<br /><br /> 位於 HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBC. 的值INI\ODBC File DSN\DefaultDSNDir 指定 ODBC 資料來源管理員在建立以檔案為基礎的資料來源時所使用的預設位置。<br /><br /> 例如：<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 開放式資料庫連接（ODBC）](../odbc/microsoft-open-database-connectivity-odbc.md)
