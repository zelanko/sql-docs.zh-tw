---
title: 驅動程式規格子機碼 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f5523c54286ed2e7cc554745dc269599115793e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094170"
---
# <a name="driver-specification-subkeys"></a>驅動程式規格子機碼
ODBC 驅動程式子機碼中所列每個驅動程式都有自己的子機碼。 這個子機碼有相同名稱下的 ODBC 驅動程式子機碼的對應值。 這個子機碼底下的值清單的驅動程式和驅動程式安裝程式 Dll，所傳回的驅動程式關鍵字值的完整路徑**SQLDrivers**，並使用計數。 值的格式是下表所示。  
  
|名稱|資料類型|Data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**N**}{**Y**&#124;**N**}{**Y**&#124;**N**}|  
|CreateDSN|REG_SZ|*driver-description*|  
|驅動程式|REG_SZ|*driver-DLL-path*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *檔案 extension1*[ **，\*。** *檔案 extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|安裝程式|REG_SZ|*setup-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*計數*|  
  
 下表顯示每個關鍵字的使用。  
  
|關鍵字|使用量|  
|-------------|-----------|  
|**APILevel**|數字，表示 ODBC 介面驅動程式支援的一致性層級：<br /><br /> 0 = 無<br /><br /> 1 = 受支援的層級 1<br /><br /> 2 = 層級 2 支援<br /><br /> 這必須是 SQL_ODBC_INTERFACE_CONFORMANCE 選項中所傳回的值相同**SQLGetInfo**。|  
|**CreateDSN**|若要安裝驅動程式時，會建立一或多個資料來源的名稱。 系統資訊必須包含一個資料來源規格 區段中列出的每個資料來源**CreateDSN**關鍵字。 不應該包含下列各節**驅動程式**關鍵字，因為這是區段中指定驅動程式規格，但必須包含足夠的資訊**ConfigDSN**驅動程式中的函式安裝程式 DLL，而不會顯示任何對話方塊建立資料來源的規格。 如需資料來源規格區段的格式，請參閱[資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)。|  
|**ConnectFunctions**|三個字元字串，表示驅動程式是否支援**SQLConnect**， **SQLDriverConnect**，並**SQLBrowseConnect**。 如果此驅動程式支援**SQLConnect**，第一個字元是"Y"; 否則它是"N"。 如果此驅動程式支援**SQLDriverConnect**，第二個字元是"Y"; 否則它是"N"。 如果此驅動程式支援**SQLBrowseConnect**，第三個字元是"Y"; 否則它是"N"。 比方說，如果驅動程式支援**SQLConnect**並**SQLDriverConnect**而非**SQLBrowseConnect**，三個字元的字串是"YYN 」。|  
|**DriverODBCVer**|ODBC 驅動程式支援的版本與字元字串。 版本是表單*nn.nn*、 前兩個數字都是主要的版本而接下來的兩位數的次要版本。 如需本手冊中所述的 ODBC 版本，驅動程式必須傳回 「 03.00"。<br /><br /> 這必須是 SQL_DRIVER_ODBC_VER 選項中所傳回的值相同**SQLGetInfo**。|  
|**FileExtns**|檔案為基礎的驅動程式，以逗號分隔清單的檔案副檔名的驅動程式可以使用。 比方說，dBASE 驅動程式可能會指定\*.dbf 和格式化的文字檔驅動程式可能會指定\*.txt\*.csv。 如需範例應用程式如何使用這項資訊，請參閱**FileUsage**關鍵字。|  
|**FileUsage**|數字，指出檔案為基礎的驅動程式如何直接處理資料來源中的檔案。<br /><br /> 0 = 驅動程式不是檔案為基礎的驅動程式。 例如，ORACLE 驅動程式是以 DBMS 為基礎的驅動程式。<br /><br /> 1 = 資料表中的資料來源檔案為基礎的驅動程式視為檔案。 比方說，Xbase 驅動程式會將每個 Xbase 檔案視為資料表中。<br /><br /> 2 = 為類別目錄的資料來源中的檔案為基礎的驅動程式視為檔案。 例如，Microsoft® Access 驅動程式會將每個 Microsoft Access 檔案視為完整的資料庫中。<br /><br /> 應用程式可能會以此判斷使用者如何選取資料。 比方說，Xbase 和 Paradox 使用者通常將資料儲存在檔案中，而 ORACLE 和 Microsoft Access 的使用者通常將資料視為儲存在資料表中。<br /><br /> 當使用者選取**開啟資料檔**從**檔案**功能表中，應用程式可以顯示**開啟 Windows 檔案**通用對話方塊。 檔案類型的清單會使用具有指定的檔案副檔名**FileExtns**關鍵字，以指定的驅動程式**FileUsage**值為 1 和"Y"做為第二個值的字元**ConnectFunctions**關鍵字。 應用程式在使用者選取檔案之後，會呼叫 **SQLDriverConnect** 具有 **驅動程式** 關鍵字，然後執行 **選取** \*FROM *資料表名稱* 陳述式。<br /><br /> 當使用者選取**匯入資料**從**檔案**功能表中，應用程式可以顯示一份指定的驅動程式的描述**FileUsage**值為 0 或 2，且"Y"做為第二個值的字元**ConnectFunctions**關鍵字。 應用程式在使用者選取的驅動程式之後，會呼叫**SQLDriverConnect**具有**驅動程式**關鍵字，然後顯示自訂**選取表格** 對話方塊。|  
|**SQLLevel**|數字，指出驅動程式所支援的 SQL-92 文法：<br /><br /> 0 = SQL-92 項目<br /><br /> 1 = FIPS127 2 過渡期<br /><br /> 2 = SQL-92 中繼<br /><br /> 3 = SQL-92 完整<br /><br /> 這必須是 SQL_SQL_CONFORMANCE 選項中所傳回的值相同**SQLGetInfo**。|  
  
 如需使用方式計數資訊，請參閱[使用量計算](../../../odbc/reference/install/usage-counting.md)稍早在這一節。  
  
 應用程式不應該設定的使用計數。 ODBC 會維護此計數。  
  
 比方說，假設已格式化的文字檔案的驅動程式具有驅動程式名為 Text.dll DLL，不同的驅動程式安裝程式 DLL 名為 Txtsetup.dll，並已安裝三次。 如果驅動程式支援層級 1 API 一致性層級，支援 Minimum SQL 文法的一致性層級，會將檔案視為資料表，而且可以使用.txt 和.csv 副檔名的檔案，底下的文字子機碼的值可能，如下所示：  
  
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
