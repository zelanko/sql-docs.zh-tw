---
title: 以程式設計方式設定悖論驅動程式的選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d04de1f0de4baca5b3f474ef9fbcf3f886e6906f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300758"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以程式設計方式設定 Paradox 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|目錄|設置目標目錄。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的調用中的**DEFAULTDIR**關鍵字。|  
|整理序列|欄位排序的順序。<br /><br /> 序列可以是 ASCII(預設值)、國際、瑞典-芬蘭文或挪威-丹麥文。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)中的**COLLATINGSEQUENCE**關鍵字。|  
|描述|數據源中數據的可選說明;例如,「僱用日期、工資歷史記錄和所有員工的當前審核。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)調用中的 **「描述**」關鍵字。|  
|獨佔|如果選擇了 **「獨佔」** 框,則資料庫將在獨佔模式下打開,並且一次只能由一個用戶訪問。 在獨佔模式下運行時,性能會增強。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)調用中的**EXCLUSIVE**關鍵字。|  
|淨樣式|訪問悖論數據時要使用的網路訪問樣式:"3.x",*x*表示悖論 3。*x*或"4。*x"* 為悖論4。*x*或 5。*x*. . 可以設置為"3"。*x"* 或"4。*x"* 如果版本是悖論4。*x*或 5。*x;* 如果版本是悖論 3。*x*,樣式必須為"3"。*x"。*|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的調用中的**PARADOXNETSTYLE**關鍵字。|  
|頁面逾時|指定頁面(如果不使用)在刪除之前保留在緩衝區中的時間段(以十分之一秒表示)。 默認值為 600 秒(60 秒)。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 由於固有的延遲,頁面超時不能為 0。 即使頁面超時選項設置為低於該值,頁面超時也不能小於固有的延遲。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)中的**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀資料庫。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的調用中的**READONLY**關鍵字。|  
|選擇目錄|顯示一個對話框,您可以在其中選擇包含要存取的檔案的目錄。<br /><br /> 定義數據源目錄時,指定最常用的檔案所在的目錄。 ODBC 驅動程式使用此目錄作為預設目錄。 如果經常使用其他檔,則將其複製到此目錄中。 或,您可以在 SELECT 語句中限定具有目錄名稱的檔名:<br /><br /> 從\*C 選擇:[MYDIR_EMP<br /><br /> 或者,您可以使用**SQLSetConnectOption**函數使用SQL_CURRENT_QUALIFIER選項來指定新的預設目錄。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的調用中的**DEFAULTDIR**關鍵字。|  
|選擇網路目錄|包含 Paradox 鎖資料庫的目錄的完整路徑,因為它包含Pdoxusrs.net檔(在悖論 4 中)。*x*) 或Paradox.net檔(在悖論 5 中)。*x*)。 如果目錄不包含這些檔之一,則 Paradox 驅動程式將創建一個。 有關這些文件的資訊,請參閱 Paradox 文檔。<br /><br /> 在選擇網路目錄之前,必須在**使用者名**文字框中輸入 Paradox 使用者名。 按下 **「選擇網路目錄**」以選擇網路目錄。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的調用中的**PARADOXNETPATH**關鍵字。|  
|使用者名稱|悖論使用者名。 這是遇到鎖時向 Paradox 檔的其他用戶顯示的名稱。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)中的**PARADOXUSERNAME**關鍵字。|
