---
title: 以程式設計方式設定存取驅動程式的選項 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a90f0a20569a2a0a5bb93dec7aa4b95b50093dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300788"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以程式設計方式設定 Access 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|緩衝區大小|Microsoft Access 用於將數據傳輸到磁碟和從磁碟傳輸的內部緩衝區(以千位元組為單位)的大小。 默認緩衝區大小為 2048 KB(顯示為 2048)。 可以輸入任何被 256 整數整數值可分割。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的 MAXBUFFERSIZE 關鍵字。|  
|資料來源名稱|標識數據源的名稱,如工資單或人員。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**DSN**關鍵字。|  
|資料庫|無需選擇或創建資料庫即可設置 Microsoft Access 資料來源。 如果在設定時未提供資料庫,則在連接到數據源時將提示使用者選擇資料庫檔。|要動態設定這個選項,請使用**DBQ**關鍵字呼叫[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|描述|數據源中數據的可選說明;例如,「僱用日期、工資歷史記錄和所有員工的當前審核。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)調用中的 **「描述**」關鍵字。|  
|獨佔|如果選擇了 **「獨佔」** 框,則資料庫將在獨佔模式下打開,並且一次只能由一個用戶訪問。 在獨佔模式下運行時,性能會增強。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)調用中的**EXCLUSIVE**關鍵字。|  
|隱含提交同步|確定如何在事務外部所做的更改寫入資料庫。 此值最初設置為"是",這意味著 Microsoft Access 驅動程式將等待內部/隱式事務中的提交完成。|這個選項包含在 Microsoft 存取驅動程式的 **「設定進階選項**」對話框中。|  
|頁面逾時|指定頁面(如果不使用)在刪除之前保留在緩衝區中的時間段(以毫秒為單位)。 對於 Microsoft Access 驅動程式,預設值為 500 毫秒(0.5 秒)。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 由於固有的延遲,頁面超時不能為 0。 即使頁面超時選項設置為低於該值,頁面超時也不能小於固有的延遲。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀資料庫。|要動態設定此選項,請使用對[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)的調用中的**READONLY**關鍵字。|  
|系統資料庫|要與要存取的Microsoft Access資料庫一起使用的Microsoft Access系統資料庫的完整路徑。<br /><br /> 按下 **「系統資料庫**」 按鈕以選擇要使用的系統資料庫。 ODBC 微軟存取驅動程式提示使用者輸入使用者名和密碼。 預設名稱為"管理員",管理員使用者的 Microsoft Access 中的預設密碼為空字串。<br /><br /> 要提高 Microsoft Access 資料庫的安全性,請創建新使用者以替換管理員使用者並刪除管理員使用者,或更改管理員使用者有權存取的物件。|要動態設定此選項,請使用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)調用中的**SYSTEMDB**關鍵字。|  
|Threads|發動機要使用的後台線程數。 對於 Microsoft Access 驅動程式,此值預設為 3,但可以更改。 如果資料庫中存在大量活動,使用者可能希望增加線程數。<br /><br /> 這個選項包含在 Microsoft 存取驅動程式的 **「設定進階選項**」對話框中。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**THREADS**關鍵字。|  
|使用者提交同步|確定 Microsoft Access 驅動程式是否會非同步執行繪式使用者定義的事務。 此值最初設置為"是",這意味著 Microsoft Access 驅動程式將等待使用者定義的事務中的提交完成。<br /><br /> 將此選項設置為 False 可能會在多用戶環境中產生不可預知的後果。|要動態設定此選項,請使用調用[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)中的**USERCOMMITSYNC**關鍵字。|
