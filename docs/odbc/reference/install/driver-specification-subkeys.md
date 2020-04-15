---
title: 驅動程式規格子鍵 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47aa75f647e5fd8a88168611a3b21284962c70a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280578"
---
# <a name="driver-specification-subkeys"></a>驅動程式規格子機碼
ODBC 驅動程式子鍵中列出的每個驅動程式都有其自己的子鍵。 此子鍵的名稱與 ODBC 驅動程式子鍵下的相應值相同。 此子鍵下的值列出了驅動程式和驅動程式設置 DLL 的完整路徑 **、SQLDriver**返回的驅動程式關鍵字的值以及使用方式計數。 值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|API 等級|REG_SZ|**0** &#124; **1** &#124; **2**|  
|連線功能|REG_SZ|[**Y**&#124;**N****]** Y&#124;**N**=**Y**&#124;**N**||  
|建立DSN|REG_SZ|*驅動程式描述*|  
|驅動程式|REG_SZ|*驅動程式-DLL 路徑*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|檔案 Extns|REG_SZ|**\*.** *檔案副檔名1*=**\*。** *檔案副檔名2*|...|  
|檔案使用|REG_SZ|**0** &#124; **1** &#124; **2**|  
|安裝程式|REG_SZ|*設定-DLL路徑*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|使用方式計數|REG_DWORD|*count*|  
  
 下表顯示了每個關鍵字的使用。  
  
|關鍵字|使用量|  
|-------------|-----------|  
|**API 等級**|指示驅動程式支援的 ODBC 介面一致性等級的數位:<br /><br /> 0 = 無<br /><br /> 1 = 支援 1 級<br /><br /> 2 = 支援 2 級<br /><br /> 這必須與**SQLGetInfo**中SQL_ODBC_INTERFACE_CONFORMANCE選項返回的值相同。|  
|**建立DSN**|安裝驅動程式時要建立的一個或多個資料源的名稱。 系統資訊必須包含一個數據源規範部分,用於**使用CreateDSN**關鍵字列出的每個資料源。 這些節不應包括**Driver**關鍵字,因為這在驅動程式規範部分中指定,但必須在驅動程式設置 DLL 中包含足夠的**ConfigDSN**函數的資訊,以創建數據源規範而不顯示任何對話方塊。 關於資料來源規範部份的格式,請參考[資料來源的資料 。](../../../odbc/reference/install/data-source-specification-subkeys.md)|  
|**連線功能**|三字串, 指示驅動程式是否支援**SQLConnect、SQLDriverConnect**與**SQLBrowseConnect**。 **SQLConnect** 如果驅動程式支援**SQLConnect,** 則第一個字元為"Y";如果驅動程式支援 SQLConnect,則第一個字元為"Y"。",則為"Y"。",則為"Y"。",則為否則,它是"N"。 如果驅動程式支援**SQLDriverConnect,** 則第二個字元為"Y";如果驅動程式支援 SQLDriverConnect,則第二個字元為"Y"。",則為"Y"。",則為"Y"。",則為"否則,它是"N"。 如果驅動程式支援**SQLBrowseConnect,** 則第三個字元為"Y";如果驅動程式支援 SQLBrowseConnect,則第三個字元為"Y"。",則為"Y"。",則為"Y"。",則為"否則,它是"N"。 例如,如果驅動程式支援**SQLConnect**和**SQLDriverConnect,** 但不支援**SQLBrowseConnect,** 則三個字元字串為"YYN"。|  
|**DriverODBCVer**|具有驅動程式支援的 ODBC 版本的字串。 版本是形式*nn.nn,* 其中前兩位數位是主要版本,接下來的兩位數位是次要版本。 對於本手冊中描述的 ODBC 版本,驅動程式必須返回"03.00"。<br /><br /> 這必須與**SQLGetInfo**中SQL_DRIVER_ODBC_VER選項返回的值相同。|  
|**檔案 Extns**|對於基於檔案的驅動程式,驅動程式可以使用的檔案擴展名的逗號分隔清單。 例如,dBASE 驅動程式可能\*指定 .dbf,格式化的文本文件驅動程式\*可能指定 .txt..csv。\* 有關應用程式如何使用此資訊的範例,請參閱**檔使用**關鍵字。|  
|**檔案使用**|指示基於檔的驅動程式如何處理數據來源中的檔案的數位。<br /><br /> 0 = 驅動程式不是基於檔的驅動程式。 例如,ORACLE 驅動程式是基於 DBMS 的驅動程式。<br /><br /> 1 = 基於檔案的驅動程式將資料來源中的檔案視為表。 例如,Xbase 驅動程式將每個 Xbase 檔案視為表。<br /><br /> 2 = 基於檔案的驅動程式將資料來源中的檔案視為目錄。 例如,Microsoft®存取驅動程式將每個 Microsoft Access 檔案視為一個完整的資料庫。<br /><br /> 應用程式可能用它來確定使用者如何選擇數據。 例如,Xbase 和 Paradox 使用者通常認為資料儲存在檔中,而 ORACLE 和 Microsoft Access 使用者通常認為數據存儲在表中。<br /><br /> 當使用者從 **「檔案**」功能表中選擇 **「打開的資料檔」** 時,應用程式可以顯示**Windows 檔打開**通用對話框。 檔案類型清單將使用**FileExtns**關鍵字指定的檔副檔名,用於指定**FileUse**值 1 和「Y」作為**ConnectFunctions**關鍵字值的第二個字元的驅動程式。 使用者選擇檔案後,應用程式將使用**DRIVER**關鍵字調用**SQLDriverConnect,** 然後執行**\*SELECT FROM*表名*** 語句。<br /><br /> 當使用者從 **「檔案」** 選單中選擇 **「匯入資料**」時,應用程式可以顯示指定**檔案使用**值 0 或 2 的驅動程式的說明清單,以及作為**ConnectFunctions**關鍵字值的第二個字元的「Y」的說明清單。 使用者選擇驅動程式後,應用程式將使用**DRIVER**關鍵字調用**SQLDriverConnect,** 然後顯示自定義**選擇表**對話方塊。|  
|**SQLLevel**|指示驅動程式支援的 SQL-92 語法的數位:<br /><br /> 0 = SQL-92 條目<br /><br /> 1 = FIPS127-2 過渡<br /><br /> 2 = SQL-92 中間<br /><br /> 3 = SQL-92 完整<br /><br /> 這必須與**SQLGetInfo**中SQL_SQL_CONFORMANCE選項返回的值相同。|  
  
 有關使用方式計數的資訊,請參閱本節前面[先查看使用方式計數](../../../odbc/reference/install/usage-counting.md)。  
  
 應用程式不應設置使用計數。 ODBC 將保留此計數。  
  
 例如,假設格式化文本檔的驅動程式具有名為 Text.dll 的驅動程式 DLL,一個單獨的驅動程式設置 DLL 名為 Txtsetup.dll,並且已安裝三次。 如果驅動程式支援等級 1 API 一致性級別,支援最小 SQL 語法一致性級別,將檔案視為表,並且可以使用具有 .txt 和 .csv 擴展名的檔案,則 Text 子鍵下的值可能如下所示:  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
