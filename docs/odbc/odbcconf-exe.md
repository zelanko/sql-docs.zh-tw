---
title: 藥點。EXE |微軟文件
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
ms.openlocfilehash: d771f01d292312f8a0f0060c16e3c348bf2e009e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307529"
---
# <a name="odbcconfexe"></a>藥點。Exe
ODBCCONF.exe 是一個命令列工具,允許您配置 ODBC 驅動程式和數據源名稱。  
  
> [!NOTE]  
>  ODBCCONF.exe 將在將來版本的 Windows 數據訪問元件中刪除。 避免使用此功能,並計畫修改當前使用此功能的應用程式。 您可以使用 PowerShell 命令來管理驅動程式和資料來源。 有關這些 PowerShell 指令的詳細資訊,請參閱[Windows 資料存取元件 cmdlet](/powershell/module/wdac)。  
  
## <a name="syntax"></a>語法  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>引數  
 *開關*  
 零個或多個開關選項。 有關可用交換機的清單,請參閱本主題後面的備註部分。  
  
 *action*  
 要執行一個操作。 有關可用選項的清單,請參閱備註部分。  
  
## <a name="remarks"></a>備註  
 以下交換器可用:  
  
|Switch|描述|  
|------------|-----------------|  
|/A =*操作*||指定操作。<br /><br /> 如果只指定一個操作,則 /A 是可選的。|  
|/?|顯示 ODBCCONF 的使用方式。Exe。|  
|/C|如果操作失敗,處理將繼續。|  
|/E|處理完成後,擦除使用 /F 指定的回應檔。|  
|/F|使用回應檔案,如`odbcconf /F my.rsp`。<br /><br /> 我的.rsp 可能如下所示:`REGSVR c:\my.dll`<br /><br /> /A 不在回應檔中使用。|  
|/H|顯示使用方式(説明)。 此開關與 /? 相同。|  
|/L+*模式*=*檔案名稱*|以三種模式之一將程式輸出發送到檔案:普通 (n)、詳細 (v) 和調試 (d)。 除錯模式記錄由 odbcconf.exe 載入的 DLL。<br /><br /> 如果指定 /L 而不帶模式,日誌檔將為空。<br /><br /> 例如 **,/Lv log.txt**。|  
|/R|重新啟動後將執行該操作。|  
|/S|無訊息模式。 不顯示錯誤消息。|  
  
 可用的動作如下：  
  
|動作|描述|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name_特定於驅動程式的設定參數*|載入相應的驅動程式設定 DLL 並調用**ConfigDriver**函數。<br /><br /> 等效於[SQLConfig 驅動程式函數](../odbc/reference/syntax/sqlconfigdriver-function.md)。<br /><br /> 例如：<br /><br /> /A [CONFIGDRIVER " 驅動程式名稱" "CPTimeout=60"]<br /><br /> /A [CONFIGDRIVER " 驅動程式名稱' "驅動程式+03.80"]|  
|CONFIGDSN *driver_name* DSN_*名稱*&#124;*屬性*|添加或修改系統數據源。<br /><br /> 等效於[SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A [CONFIGDSN"SQL 伺服器""DSN_名稱&#124;伺服器_srv"]|  
|CONFIGSYSDSN *driver_name* DSN**名稱*&#124;*屬性*|添加或修改系統數據源。<br /><br /> 等效於[SQLConfigDataSource 函數](../odbc/reference/syntax/sqlconfigdatasource-function.md)。<br /><br /> 例如：<br /><br /> /A [CONFIGSYSDSN"SQL 伺服器""DSN_名稱&#124;伺服器=srv"]|  
|安裝驅動程式|等效於[SQLInstallDriverEx 函數](../odbc/reference/syntax/sqlinstalldriverex-function.md)。<br /><br /> 有關傳遞給 INSTALLDRIVER 的關鍵字-值對語法的資訊,請參閱[驅動程式規範子鍵](../odbc/reference/install/driver-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> /A [SETUPDRIVER"您的驅動程式&#124;驅動程式\c:\&#124;安装程序\c:\您的.dll &#124; APILevel_2 &#124;连接功能_YYy&#124;驅動程式ODBCVer_03.50 &#124;文件使用情况{0 &#124; SQLLevel_1"]|  
|安裝*轉換器設定_驅動程式路徑*|將有關轉換器的資訊添加到**HKEY_LOCAL_MACHINE_軟體_ODBC_ODBCINST。INI_ODBC 譯員**註冊表項。<br /><br /> 等效於[SQLInstall 翻譯器Ex 函數](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。<br /><br /> 有關傳遞給 INSTALLDRIVER 的關鍵字-值對語法的資訊,請參考[翻譯器的螢幕鍵](../odbc/reference/install/translator-specification-subkeys.md)。<br /><br /> 例如：<br /><br /> /A [安裝翻譯&#124;翻譯器\c:\my.dll &#124;安装程序\c:\my.dll"]|  
|REGSVR *dll*|註冊 DLL。<br /><br /> 等效於 regsvr32.exe。<br /><br /> 例如：<br /><br /> /A [REGSVR c:[my.dll]|  
|塞特·拉迪斯納爾迪|當HKEY_LOCAL_MACHINE_軟體_ODBC_ODBC時。INI_ODBC 檔案 DSN_預設DSNDir不存在,SETFILEDSNDIR 操作將創建它,並在HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_Windows_當前版本_常見檔Dir處為其分配值,並附加了 [ODBC_數據源》。<br /><br /> HKEY_LOCAL_MACHINE_軟體_ODBC_ODBC處的值。INI_ODBC 檔案 DSN_預設 DSNDir 指定 ODBC 資料來源管理員在建立基於檔案的資料來源時使用的預設位置。<br /><br /> 例如：<br /><br /> /A [SETFILEDSNDIR]|  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 開放式資料庫連接 (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
