---
title: 以程式設計方式設定文字檔案驅動程式的選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e19c3b49479047bc92a7b6f72359d4951d8df16e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300748"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>以程式設計方式設定文字檔驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|資料來源名稱|標識數據源的名稱,如工資單或人員。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)中的**DSN**關鍵字。|  
|定義格式|顯示 **「定義文字格式」** 對話框,並使您能夠在資料源目錄中指定各個表的架構。|此選項不能透過呼叫[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)動態設定。|  
|描述|數據源中數據的可選說明;例如,「僱用日期、工資歷史記錄和所有員工的當前審核。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)調用中的 **「描述**」關鍵字。|  
|目錄|選擇目標目錄。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的調用中的**DEFAULTDIR**關鍵字。|  
|延伸清單|列出資料來源上文字檔的檔案名副檔名。 使用 Text 驅動程式時,當使用沒有擴充名的名稱執行 CREATE TABLE 語句時,將創建一個沒有擴充名的檔案。 其他驅動程式在未提供擴展名時創建具有預設擴展名的檔。 要建立具有 .txt 副檔名的文件,必須將擴展名包含在名稱中。 要在 **「定義文字格式」** 對話方塊「*」中顯示沒有副檔名的檔案。 必須添加到擴展清單中。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的呼叫中的 **「擴展S」** 關鍵字。|  
|唯讀|將資料庫指定為唯讀資料庫。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的調用中的**READONLY**關鍵字。|  
|要掃描的列|要掃描以確定每列數據類型的行數。 給定找到的最大數據類型數,確定數據類型。 如果遇到的數據與為列猜到的數據類型不匹配,則數據類型將作為 NULL 值返回。<br /><br /> 對於 Text 驅動程式,您可以輸入從 1 到 32767 的數位,以便掃描的行數;但是,該值將始終預設為 25。 (超出限制的數位將返回錯誤。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)中的**MAXSCANROWS**關鍵字。|  
|選擇目錄|顯示一個對話框,您可以在其中選擇包含要存取的檔案的目錄。<br /><br /> 定義數據源目錄時,指定最常用的檔案所在的目錄。 ODBC 驅動程式使用此目錄作為預設目錄。 如果經常使用其他檔,則將其複製到此目錄中。 或,您可以在 SELECT 語句中限定具有目錄名稱的檔名:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> 或者,您可以使用**SQLSetConnectOption**函數使用SQL_CURRENT_QUALIFIER選項來指定新的預設目錄。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)的調用中的**DEFAULTDIR**關鍵字。|
