---
title: "驅動程式規格子機碼 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f45130c81f9fc4f669cf95d4bde72155f519c1aa
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specification-subkeys"></a>驅動程式規格子機碼
ODBC 驅動程式的子機碼中列出的每個驅動程式都有自己的子機碼。 這個子機碼有同名的 ODBC 驅動程式的子機碼下的對應值。 這個子機碼下的值清單之驅動程式和驅動程式安裝程式所傳回的驅動程式關鍵字值的 Dll 的完整路徑**SQLDrivers**，和使用方式計數。 值的格式是下表所示。  
  
|名稱|資料類型|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**N**} {**Y**&#124;**N**} {**Y**&#124;**N**}|  
|CreateDSN|REG_SZ|*驅動程式說明*|  
|驅動程式|REG_SZ|*驅動程式 DLL 路徑*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *檔案 extension1*[**，\*。** *檔案 extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|安裝程式|REG_SZ|*安裝程式 DLL 路徑*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*計數*|  
  
 下表顯示每個關鍵字的使用。  
  
|關鍵字|使用方式|  
|-------------|-----------|  
|**APILevel**|數字，表示 ODBC 介面驅動程式支援的一致性層級：<br /><br /> 0 = 無<br /><br /> 1 = 支援層級 1<br /><br /> 2 = 支援層級 2<br /><br /> 這必須是 SQL_ODBC_INTERFACE_CONFORMANCE 選項中所傳回的值相同**SQLGetInfo**。|  
|**CreateDSN**|若要安裝驅動程式時，會建立一或多個資料來源的名稱。 系統資訊必須包含一個資料來源規格 > 一節列出與每個資料來源**CreateDSN**關鍵字。 這些區段不應包含**驅動程式**關鍵字，因為這指定在驅動程式規格區段中，但必須包含足夠的資訊讓**ConfigDSN**驅動程式中的函式安裝程式的 DLL，以便建立資料來源的規格，而不會顯示任何對話方塊。 針對資料來源規格區段的格式，請參閱[資料來源規格子機碼](../../../odbc/reference/install/data-source-specification-subkeys.md)。|  
|**ConnectFunctions**|三個字元字串，表示驅動程式是否支援**SQLConnect**， **SQLDriverConnect**，和**SQLBrowseConnect**。 如果驅動程式支援**SQLConnect**，第一個字元為"Y"，否則便是"N"。 如果驅動程式支援**SQLDriverConnect**，第二個字元為"Y"，否則便是"N"。 如果驅動程式支援**SQLBrowseConnect**，第三個字元為"Y"，否則便是"N"。 例如，如果驅動程式支援**SQLConnect**和**SQLDriverConnect**但不是**SQLBrowseConnect**，三個字元字串是 「 YYN"。|  
|**DriverODBCVer**|ODBC 驅動程式支援的版本字串的字元字串。 版本是表單的*nn.nn*，其中前兩個數字的主要版本，而下面兩個位數的次要版本。 如需本手冊中所述的 ODBC 版本，此驅動程式必須傳回"03.00"。<br /><br /> 這必須是 SQL_DRIVER_ODBC_VER 選項中所傳回的值相同**SQLGetInfo**。|  
|**FileExtns**|以檔案為基礎的驅動程式，以逗號分隔清單的檔案副檔名的驅動程式可以使用。 例如，可能會指定 dBASE 驅動程式\*.dbf 和格式化的文字檔案驅動程式可能會指定\*.txt，\*.csv。 應用程式如何使用這項資訊的範例，請參閱**FileUsage**關鍵字。|  
|**FileUsage**|數字，指出如何以檔案為基礎的驅動程式直接處理的資料來源中的檔案。<br /><br /> 0 = 不是以檔案為基礎的驅動程式。 例如，ORACLE 驅動程式是 DBMS 架構驅動程式。<br /><br /> 1 = 資料來源中的檔案為基礎的驅動程式會視為檔案，做為資料表。 比方說，Xbase 驅動程式會將每個 Xbase 檔案視為資料表中。<br /><br /> 2 = 資料來源為類別目錄中檔案為基礎的驅動程式會視為檔案。 例如，Microsoft® Access 驅動程式會將每個 Microsoft Access 檔案視為完整的資料庫。<br /><br /> 應用程式可以將此來決定使用者如何選取資料。 例如，Xbase 和 Paradox 使用者通常將資料儲存在檔案中，而 ORACLE 和 Microsoft Access 的使用者通常將資料視為儲存在資料表中。<br /><br /> 當使用者選取**開啟資料檔**從**檔案**功能表上，應用程式無法顯示**Windows 檔案開啟**通用對話方塊。 檔案類型的清單會使用具有指定的檔案副檔名**FileExtns**關鍵字指定的驅動程式**FileUsage** 1 和"Y"做為值的第二個字元的值**ConnectFunctions**關鍵字。 應用程式在使用者選取檔案之後，會呼叫**SQLDriverConnect**與**驅動程式**關鍵字，然後執行**選取\*FROM*資料表名稱*** 陳述式。<br /><br /> 當使用者選取**匯入資料**從**檔案**功能表上，應用程式無法顯示說明指定的驅動程式的清單**FileUsage**值為 0 或 2，且"Y"做為值的第二個字元**ConnectFunctions**關鍵字。 應用程式在使用者選取的驅動程式之後，會呼叫**SQLDriverConnect**與**驅動程式**關鍵字，然後顯示自訂**選取資料表** 對話方塊。|  
|**SQLLevel**|數字，指出 SQL 92 文法的驅動程式支援：<br /><br /> 0 = SQL 92 項目<br /><br /> 1 = FIPS127 2 過渡期<br /><br /> 2 = SQL 92 中繼<br /><br /> 3 = sql-92 完整<br /><br /> 這必須是 SQL_SQL_CONFORMANCE 選項中所傳回的值相同**SQLGetInfo**。|  
  
 如需使用方式計數資訊，請參閱[使用量計算](../../../odbc/reference/install/usage-counting.md)稍早在這一節。  
  
 應用程式不應該設定的使用計數。 ODBC 會維護這個計數。  
  
 例如，假設格式化的文字檔案的驅動程式具有驅動程式名為 Text.dll 的 DLL，不同的驅動程式安裝程式 DLL 名為 Txtsetup.dll，和已安裝三次。 如果驅動程式支援的層級 1 API 的一致性層級，支援的最小 SQL 文法一致性層級、 檔案視為資料表，而且可以使用.txt 和.csv 副檔名的檔案，文字子機碼下的值可能，如下所示：  
  
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

