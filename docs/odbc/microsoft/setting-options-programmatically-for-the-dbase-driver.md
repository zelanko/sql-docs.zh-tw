---
title: 以程式設計方式設定 dBASE 驅動程式的選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75889d9ff3ccfe01f9b8d5141df7774205522815
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300778"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以程式設計方式設定 dBASE 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|近似行計數|確定表大小統計資訊是否近似。 此選項適用於使用 ODBC 驅動程式的所有資料來源。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)調用中的**STATISTICS**關鍵字。|  
|整理序列|欄位排序的順序。<br /><br /> 序列可以是:ASCII(預設值)或國際。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)中的**COLLATINGSEQUENCE**關鍵字。|  
|資料來源名稱|標識數據源的名稱,如工資單或人員。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)中的**DSN**關鍵字。|  
|資料庫|無需選擇或創建資料庫即可設置 Microsoft Access 資料來源。 如果在設置時未提供資料庫,則使用者在連接到數據源時將提示他們選擇資料庫檔。|要動態設定這個選項,請使用**DBQ**關鍵字呼叫[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|描述|數據源中數據的可選說明;例如,「僱用日期、工資歷史記錄和所有員工的當前審核。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)調用中的 **「描述**」關鍵字。|  
|獨佔|如果選擇了 **「獨佔」** 框,則資料庫將在獨佔模式下打開,並且一次只能由一個用戶訪問。 在獨佔模式下運行時,性能會增強。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)調用中的**EXCLUSIVE**關鍵字。|  
|頁面逾時|指定頁面(如果不使用)在刪除之前保留在緩衝區中的時間段(以十分之一秒表示)。 默認值為 600 秒(60 秒)。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 由於固有的延遲,頁面超時不能為 0。 即使頁面超時選項設置為低於該值,頁面超時也不能小於固有的延遲。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)中的**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀資料庫。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的調用中的**READONLY**關鍵字。|  
|選擇目錄|顯示一個對話框,您可以在其中選擇包含要存取的檔案的目錄。<br /><br /> 定義數據源目錄時,請指定最常用的檔案所在的目錄。 ODBC 驅動程式使用此目錄作為預設目錄。 如果經常使用其他檔,則將其複製到此目錄中。 或,您可以在 SELECT 語句中限定具有目錄名稱的檔名:<br /><br /> 從\*C 選擇:[MYDIR_EMP<br /><br /> 或者,您可以使用**SQLSetConnectOption**函數使用SQL_CURRENT_QUALIFIER選項來指定新的預設目錄。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的調用中的**DEFAULTDIR**關鍵字。|  
|顯示已移除的列|指定是否可以檢索或定位已標記為已刪除的行。 如果清除,則不顯示已刪除的行;如果清除,則不顯示已刪除的行。如果選中,則刪除的行將被視為與未刪除的行相同。 預設值為清除此核取方塊。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中的**DELETED**關鍵字。|
