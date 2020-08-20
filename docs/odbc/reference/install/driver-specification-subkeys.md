---
description: 驅動程式規格子機碼
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a363335931723e33a6461b86395494153491d328
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499781"
---
# <a name="driver-specification-subkeys"></a>驅動程式規格子機碼
ODBC 驅動程式子機碼中列出的每個驅動程式都有自己的子機碼。 這個子機碼與 ODBC 驅動程式子機碼底下的對應值具有相同的名稱。 此子機碼底下的值會列出驅動程式和驅動程式安裝程式 Dll 的完整路徑、 **SQLDrivers**傳回的驅動程式關鍵字值，以及使用計數。 值的格式如下表所示。  
  
|名稱|資料類型|資料|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**N**} {**y**&#124;**n**} {**y**&#124;**N**}|  
|CreateDSN|REG_SZ|*驅動程式-描述*|  
|驅動程式|REG_SZ|*驅動程式-DLL-路徑*|  
|DriverODBCVer|REG_SZ|*nn. nn*|  
|FileExtns|REG_SZ|**\*.** *extension1*[**， \* .** *file-延伸模組 2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|安裝程式|REG_SZ|*安裝程式-DLL-路徑*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*計數*|  
  
 下表顯示每個關鍵字的使用方式。  
  
|關鍵字|使用量|  
|-------------|-----------|  
|**APILevel**|指出驅動程式支援之 ODBC 介面一致性層級的數位：<br /><br /> 0 = 無<br /><br /> 1 = 支援層級1<br /><br /> 2 = 支援層級2<br /><br /> 這必須與 **SQLGetInfo**中針對 SQL_ODBC_INTERFACE_CONFORMANCE 選項所傳回的值相同。|  
|**CreateDSN**|安裝驅動程式時所要建立的一或多個資料來源的名稱。 系統資訊必須針對以 **CreateDSN** 關鍵字列出的每個資料來源，各包含一個資料來源規格區段。 這些區段不應包含 **driver** 關鍵字，因為這是在 [驅動程式規格] 區段中指定，但必須在驅動程式安裝程式 DLL 中包含足夠的 **ConfigDSN** 函式資訊，才能建立資料來源規格，而不顯示任何對話方塊。 如需資料來源規格區段的格式，請參閱 [資料來源規格](../../../odbc/reference/install/data-source-specification-subkeys.md)子機碼。|  
|**ConnectFunctions**|三個字元的字串，指出驅動程式是否支援 **SQLConnect**、 **SQLDriverConnect**和 **SQLBrowseConnect**。 如果驅動程式支援 **SQLConnect**，則第一個字元是 "Y";否則為 "N"。 如果驅動程式支援 **SQLDriverConnect**，則第二個字元是 "Y";否則為 "N"。 如果驅動程式支援 **SQLBrowseConnect**，則第三個字元是 "Y";否則為 "N"。 例如，如果驅動程式支援 **SQLConnect** 和 **SQLDriverConnect** ，但不支援 **SQLBrowseConnect**，則三個字元的字串為 "YYN"。|  
|**DriverODBCVer**|具有驅動程式支援之 ODBC 版本的字元字串。 版本的格式為 *nn. nn*，其中前兩個數字是主要版本，而下兩個數字是次要版本。 針對此手冊中所述的 ODBC 版本，驅動程式必須傳回 "03.00"。<br /><br /> 這必須與 **SQLGetInfo**中針對 SQL_DRIVER_ODBC_VER 選項所傳回的值相同。|  
|**FileExtns**|若是以檔案為基礎的驅動程式，則是由驅動程式可使用的檔案延伸模組清單（以逗號分隔）。 例如，dBASE 驅動程式可能會指定 \* .dbf，而格式化的文字檔驅動程式可能會指定 \* .txt、 \* .csv。 如需應用程式如何使用此資訊的範例，請參閱 **FileUsage** 關鍵字。|  
|**FileUsage**|數位，指出以檔案為基礎的驅動程式如何直接處理資料來源中的檔案。<br /><br /> 0 = 驅動程式不是以檔案為基礎的驅動程式。 例如，ORACLE 驅動程式是以 DBMS 為基礎的驅動程式。<br /><br /> 1 = 以檔案為基礎的驅動程式會將資料來源中的檔案視為資料表。 例如，Xbase 驅動程式會將每個 Xbase 檔案視為資料表。<br /><br /> 2 = 以檔案為基礎的驅動程式會將資料來源中的檔案視為目錄。 例如，Microsoft® Access 驅動程式會將每個 Microsoft Access 檔案視為完整的資料庫。<br /><br /> 應用程式可能會使用這個來判斷使用者將如何選取資料。 例如，Xbase 和 Paradox 使用者通常會將資料視為儲存在檔案中，而 ORACLE 和 Microsoft Access 使用者通常會將資料視為儲存在資料表中的資料。<br /><br /> 當使用者**從 [檔案**] 功能表選取 [**開啟資料**檔] 時，應用程式可能會顯示 [ **Windows 檔案開啟**一般] 對話方塊。 檔案類型清單會針對指定**FileUsage**值為1的驅動程式使用以**FileExtns**關鍵字指定的副檔名，並使用 "Y" 作為**ConnectFunctions**關鍵字值的第二個字元。 當使用者選取檔案之後，應用程式會使用**DRIVER**關鍵字來呼叫**SQLDriverConnect** ，然後** \* 從*資料表名稱*** 語句中執行 SELECT。<br /><br /> 當使用者選取 [檔案 **] 功能表中的 [匯****入資料**] 時，應用程式可以顯示指定**FileUsage**值為0或2的驅動程式描述清單，以及輸入 "Y" 作為**ConnectFunctions**關鍵字值的第二個字元。 當使用者選取驅動程式之後，應用程式會使用**driver**關鍵字來呼叫**SQLDriverConnect** ，然後顯示自訂的 [**選取資料表**] 對話方塊。|  
|**SQLLevel**|數位，指出驅動程式支援的 SQL-92 文法：<br /><br /> 0 = SQL-92 專案<br /><br /> 1 = FIPS127-2 個過渡<br /><br /> 2 = SQL-92 中繼<br /><br /> 3 = SQL-92 Full<br /><br /> 這必須與 **SQLGetInfo**中針對 SQL_SQL_CONFORMANCE 選項所傳回的值相同。|  
  
 如需使用計數的詳細資訊，請參閱本節稍早的 [使用量計數](../../../odbc/reference/install/usage-counting.md) 。  
  
 應用程式不應該設定使用計數。 ODBC 將維持這個計數。  
  
 例如，假設格式化文字檔的驅動程式有一個名為 Text.dll 的驅動程式 DLL，另一個名為 Txtsetup.dll 的驅動程式安裝 DLL，且已安裝三次。 如果驅動程式支援層級 1 API 一致性層級、支援最小的 SQL 文法一致性層級、將檔案視為資料表，並且可以使用副檔名為 .txt 和 .csv 的檔案，則文字子機碼底下的值可能如下所示：  
  
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
