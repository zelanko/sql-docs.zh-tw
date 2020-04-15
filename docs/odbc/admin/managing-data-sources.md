---
title: 管理資料來源 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5069ac9a5babc3071c52d73d5b56b21729a5d8a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307209"
---
# <a name="managing-data-sources"></a>管理資料來源
從驅動程式的安裝程式安裝 ODBC 驅動程式後,可以為其定義一個或多個數據源。 數據源名稱 (DSN) 應提供數據的唯一描述;例如,*工資或**應付帳款*。 為目前安裝的所有驅動程式定義的使用者和系統數據來源列在**ODBC 資料來源管理員**對話框**的使用者 DSN**或**系統 DSN**選項卡中。 給定目錄中的檔案資料來源列在檔案 DSN 選項卡中;**在「檔案 DSN」** 選項卡中列出該檔資料來源。要顯示的目錄在 **「檔案 DSN」** 選項卡中的「**尋找」** 框中輸入。  
  
> [!NOTE]  
>  要管理在 64 位元平臺下連接到 32 位元驅動程式的數據源,請使用 c:_windows_sysWOW64_odbcad32.exe。 要管理連接到 64 位元驅動程式的數據源,請使用 c:_windows_system32_odbcad32.exe。 在 64 位元 Windows 8 操作系統上的**管理工具**中,有 32 位元和 64 位**元 ODBC 資料來源管理員**對話框的圖示。  
  
 如果使用 64 位元 odbcad32.exe 設定或移除連接到 32 位元驅動程式的 DSN,例如,**驅動程式執行\*Microsoft 存取 (.mdb),** 您將收到以下錯誤訊息:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 要解決此錯誤,請使用 32 位元 odbcad32.exe 設定或刪除 DSN。  
  
 數據來源將特定的ODBC驅動程式與要透過該驅動程式存取的數據關聯。 例如,您可以創建數據源以使用 ODBC dBASE 驅動程式存取硬碟或網路驅動器上特定目錄中的一個或多個 dBASE 檔。 使用 ODBC 資料來源管理員,您可以添加、修改和刪除數據來源,如下表所述。  
  
|動作|描述|  
|------------|-----------------|  
|新增資料來源|可以添加多個資料源,每個數據源將驅動程式與要使用該驅動程式訪問的某些數據相關聯。 為每個數據源指定唯一標識該數據源的名稱。 例如,如果為一組包含客戶資訊的 dBASE 檔案創建數據源,則可以將數據源命名為"客戶" 應用程式通常顯示數據源名稱供用戶選擇。<br /><br /> 添加文件數據源與添加使用者或系統數據源略有不同。 有關詳細資訊,請參閱 ODBC 數據來源管理員幫助檔。|  
|變更資料來源|根據您的要求,您可能會發現有必要重新配置數據源。 您可以通過單擊任何驅動程式設置對話方塊中的 **「設定」** 來重置選項。|  
|刪除資料來源|選擇資料源後按一下 **「刪除**」。|  
  
 有關文件資料來源的詳細資訊,請參閱[使用檔案資料來源或](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) [SQLDriverConnect 函數](../../odbc/reference/syntax/sqldriverconnect-function.md)進行連接。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)
