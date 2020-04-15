---
title: 以程式設計方式設定 Excel 驅動程式的選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fcd5542e4beee1f7c7a30d5e0ee9f2815a3f0b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300768"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以程式設計方式設定 Excel 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|資料來源名稱|標識數據源的名稱,如工資單或人員。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)中的**DSN**關鍵字。|  
|資料庫|無需選擇或創建資料庫即可設置 Microsoft Access 資料來源。 如果在設定時未提供資料庫,則在連接到數據源時將提示使用者選擇資料庫檔。|要動態設定這個選項,請使用**DBQ**關鍵字呼叫[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|描述|數據源中數據的可選說明;例如,「僱用日期、工資歷史記錄和所有員工的當前審核。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)調用中的 **「描述**」關鍵字。|  
|目錄|顯示當前選定的目錄。<br /><br /> 對於 Microsoft Excel 3.0/4.0 檔,路徑顯示標記為"目錄",而對於 Microsoft Excel 5.0、7.0 或 97 個檔,路徑顯示標記為"工作簿"。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的調用中的**DEFAULTDIR**關鍵字。|  
|唯讀|將資料庫指定為唯讀資料庫。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的調用中的**READONLY**關鍵字。|  
|要掃描的列|要掃描以確定每列數據類型的行數。 給定找到的最大數據類型數,確定數據類型。 如果遇到的數據與為列猜到的數據類型不匹配,則數據類型將作為 NULL 值返回。<br /><br /> 對於 Microsoft Excel 驅動程式,可以輸入從 1 到 16 的數位,以便對行進行掃描。 該值預設為 8;如果設置為 0,則掃描所有行。 (超出限制的數位將返回錯誤。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)中的**MAXSCANROWS**關鍵字。|  
|選擇目錄|顯示一個對話框,您可以在其中選擇包含要存取的檔案的目錄。<br /><br /> 定義數據源目錄時(對於除 Microsoft Access 之外的所有驅動程式),指定最常用的檔案所在的目錄。 ODBC 驅動程式使用此目錄作為預設目錄。 如果經常使用其他檔,則將其複製到此目錄中。 或,您可以在 SELECT 語句中限定具有目錄名稱的檔名:<br /><br /> 從\*C 選擇:[MYDIR_EMP<br /><br /> 或者,您可以使用**SQLSetConnectOption**函數使用SQL_CURRENT_QUALIFIER選項來指定新的預設目錄。<br /><br /> 對於 Microsoft Excel 3.0 或 4.0 檔,路徑顯示標記為"目錄",路徑選擇按鈕標記為"選擇目錄"。 對於 Microsoft Excel 5.0、7.0 或 97 個檔,路徑顯示標記為"工作簿",路徑選擇按鈕標記為"選擇工作簿"。 定義數據源目錄時,請指定最常用的 Microsoft Excel 檔位於 Microsoft Excel 3.0/4.0 的目錄,或為 Microsoft Excel 5.0、7.0 或 97 提供工作簿檔的目錄。 對於 Microsoft Excel 5.0、7.0 和 97,禁用了 **"當前目錄**"。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的調用中的**DEFAULTDIR**關鍵字。|
