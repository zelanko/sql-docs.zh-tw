---
title: ODBCCONF.EXE | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2b4d7b20c690a1f4d7f3b445afb8348549309e5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538203"
---
# <a name="odbcconfexe"></a>ODBCCONF.EXE
ODBCCONF.exe 是命令列工具，可讓您設定 ODBC 驅動程式和資料來源的名稱。  
  
> [!NOTE]  
>  Windows Data Access Components 的未來版本將移除 ODBCCONF.exe。 請避免使用這項功能，並規劃修改目前使用這項功能的應用程式。 您可以使用 PowerShell 命令來管理驅動程式和資料來源。 如需有關這些 PowerShell 命令的詳細資訊，請參閱[Windows Data Access Components cmdlet](https://technet.microsoft.com/library/hh771019.aspx)。  
  
## <a name="syntax"></a>語法  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>引數  
 *switches*  
 零或多個參數的選項。 如需可用參數的清單，請參閱備註 」 一節中，本主題稍後的。  
  
 *action*  
 若要執行的一個動作。 如需可用之選項的清單，請參閱 < 備註 > 一節。  
  
## <a name="remarks"></a>備註  
 可使用下列參數：  
  
|參數|描述|  
|------------|-----------------|  
|/A {*action*}|指定的動作。<br /><br /> / A 是選擇性的如果只指定一個動作。|  
|/?|顯示 ODBCCONF 使用量。EXE。|  
|/C|如果動作便會失敗，繼續進行處理。|  
|/E|清除指定 /F 處理完成時的回應檔案。|  
|/F|使用回應檔案，例如`odbcconf /F my.rsp`。<br /><br /> my.rsp 可能如下所示： `REGSVR c:\my.dll`<br /><br /> / A 不會使用回應檔案中。|  
|/H|顯示使用情況 （說明）。 這個參數等同於 /？。|  
|/L[*mode*] *filename*|將程式輸出傳送到的檔案中三種模式之一： 標準 (n)、 詳細資訊 (v) 和 偵錯 (d)。 偵錯模式記錄 odbcconf.exe 所載入的 Dll。<br /><br /> 如果您指定 /L 沒有模式時，記錄檔會是空的。<br /><br /> 例如， **/Lv log.txt**。|  
|/R|在重新開機後，就會執行此動作。|  
|/S|無訊息模式。 不會顯示錯誤訊息。|  
  
 可使用下列動作：  
  
|動作|描述|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * 驅動程式專屬的組態參數*|載入適當的驅動程式安裝程式 DLL 並呼叫**ConfigDriver**函式。<br /><br /> 相當於[SQLConfigDriver 函式](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> / A {CONFIGDRIVER [驅動程式名稱]"CPTimeout = 60"}<br /><br /> / A {CONFIGDRIVER [驅動程式名稱]"DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN=*name* &#124; *attributes*|新增或修改系統資料來源。<br /><br /> 相當於[SQLConfigDataSource 函式](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|CONFIGSYSDSN *driver_name* DSN=*name* &#124; *attributes*|新增或修改系統資料來源。<br /><br /> 相當於[SQLConfigDataSource 函式](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|/INSTALLDRIVER|相當於[SQLInstallDriverEx 函式](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 傳遞至 /INSTALLDRIVER 關鍵字-值配對語法的詳細資訊，請參閱[驅動程式規格子機碼](../odbc/reference/install/driver-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> /A {INSTALLDRIVER  "Your Driver &#124; Driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel=2 &#124; ConnectFunctions=YYY &#124; DriverODBCVer=03.50 &#124; FileUsage=0 &#124; SQLLevel=1"}|  
|INSTALLTRANSLATOR *translator configuration * * 驅動程式路徑*|將轉譯程式，以相關資訊加入**HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST。INI\ODBC 轉譯器**登錄機碼。<br /><br /> 相當於[SQLInstallTranslatorEx 函式](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 傳遞至 /INSTALLDRIVER 關鍵字-值配對語法的詳細資訊，請參閱[轉譯程式規格子機碼](../odbc/reference/install/translator-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> /A {INSTALLTRANSLATOR  "My Translator &#124; Translator=c:\my.dll &#124; Setup=c:\my.dll"}|  
|REGSVR *dll*|註冊 DLL。<br /><br /> 相當於 regsvr32.exe。<br /><br /> 例如：<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|當 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC。INI\ODBC 檔案 DSN\DefaultDSNDir 不存在，SETFILEDSNDIR 動作會加以建立，並將它指派 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir，加上 \ODBC\Data 來源處的值。<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 處的值。INI\ODBC 檔案 DSN\DefaultDSNDir 指定建立的檔案為基礎的資料來源時，所使用的 ODBC 資料來源管理員 」 中的預設位置。<br /><br /> 例如：<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 開放式資料庫連接 (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
