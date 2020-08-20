---
description: ODBCCONF.EXE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4f4af809044a46fd6df8c45c77cf1d3a7929226
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471253"
---
# <a name="odbcconfexe"></a>ODBCCONF.EXE
ODBCCONF.exe 是一種命令列工具，可讓您設定 ODBC 驅動程式和資料來源名稱。  
  
> [!NOTE]  
>  未來的 Windows 資料存取元件版本將會移除 ODBCCONF.exe。 請避免使用這項功能，並規劃修改目前使用這項功能的應用程式。 您可以使用 PowerShell 命令來管理驅動程式和資料來源。 如需這些 PowerShell 命令的詳細資訊，請參閱 [Windows Data Access Components Cmdlet](/powershell/module/wdac)。  
  
## <a name="syntax"></a>語法  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>引數  
 *開關*  
 零或多個參數選項。 如需可用參數的清單，請參閱本主題稍後的「備註」一節。  
  
 *action*  
 一個要執行的動作。 如需可用選項的清單，請參閱「備註」一節。  
  
## <a name="remarks"></a>備註  
 可用的參數如下：  
  
|Switch|描述|  
|------------|-----------------|  
|/A {*action*}|指定動作。<br /><br /> 如果只指定一個動作，則/a 是選擇性的。|  
|/?|顯示 ODBCCONF.EXE 的使用量。|  
|/C|如果動作失敗，則會繼續處理。|  
|/E|處理完成時，清除以/F 指定的回應檔。|  
|/F|使用回應檔，例如 `odbcconf /F my.rsp` 。<br /><br /> 我的 .rsp 可能看起來像這樣： `REGSVR c:\my.dll`<br /><br /> /A 不會用於回應檔中。|  
|/H|顯示使用方式 (說明) 。 此參數與/？相同。|  
|/L [*mode*] *檔案名*|以下列三種模式的其中一種，將程式輸出傳送至檔案： normal (n) 、verbose (v) 和 debug (d) 。 Debug 模式會記錄 odbcconf.exe 載入的 Dll。<br /><br /> 如果您在不使用模式的情況下指定/L，記錄檔將會是空的。<br /><br /> 例如， **/Lv log.txt**。|  
|/R|動作將會在重新開機之後執行。|  
|/S|無訊息模式。 不要顯示錯誤訊息。|  
  
 以下是可用的動作：  
  
|動作|描述|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * 驅動程式專用的設定參數*|載入適當的驅動程式安裝 DLL，並呼叫 **ConfigDriver** 函數。<br /><br /> 相當於 [SQLConfigDriver 函數](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGDRIVER "Driver Name" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "Driver Name" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*name* &#124; *屬性*|新增或修改系統資料來源。<br /><br /> 相當於 [SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|CONFIGSYSDSN *driver_name* DSN =*name* &#124; *屬性*|新增或修改系統資料來源。<br /><br /> 相當於 [SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|INSTALLDRIVER|相當於 [SQLInstallDriverEx 函數](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 如需傳遞給 INSTALLDRIVER 的關鍵字-值組語法的詳細資訊，請參閱 [驅動程式規格](../odbc/reference/install/driver-specification-subkeys.md)子機碼。<br /><br /> 例如：<br /><br /> /A {INSTALLDRIVER "您的驅動程式 &#124; 驅動程式 =c:\your.dll &#124; 安裝程式 =c:\your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}|  
|INSTALLTRANSLATOR *translator configuration * * 驅動程式路徑*|將翻譯工具的相關資訊新增至 **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI \Odbc 轉譯** 程式登錄機碼。<br /><br /> 相當於 [SQLInstallTranslatorEx 函數](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 如需傳遞給 INSTALLDRIVER 的關鍵字-值組語法的詳細資訊，請參閱 [Translator 規格](../odbc/reference/install/translator-specification-subkeys.md)子機碼。<br /><br /> 例如：<br /><br /> /A {INSTALLTRANSLATOR "我的翻譯工具 &#124; Translator =c:\my.dll &#124; 設定 =c:\my.dll"}|  
|REGSVR *dll*|註冊 DLL。<br /><br /> 相當於 regsvr32.exe。<br /><br /> 例如：<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|當 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI \ODBC 檔 DSN\DefaultDSNDir 不存在時，SETFILEDSNDIR 動作將會建立該檔案，並為它指派位於 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir，並附加 \ODBC\Data 來源的值。<br /><br /> 在 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI \ODBC 檔 DSN\DefaultDSNDir 的值會指定 ODBC 資料來源系統管理員在建立檔案型資料來源時所使用的預設位置。<br /><br /> 例如：<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 開放式資料庫連接 (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
