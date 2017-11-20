---
title: "DBASE 驅動程式的選項以程式設計方式設定 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2760e0b08417121e765582904565461501eb0df6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>選項以程式設計方式設定為 dBASE 驅動程式
|選項|Description|方法|  
|------------|-----------------|------------|  
|近似資料列計數|判斷是否會計算資料表大小的統計資料值。 此選項適用於使用 ODBC 驅動程式的所有資料來源。|若要以動態方式設定這個選項，使用**統計資料**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|定序順序|欄位排序順序。<br /><br /> 序列可以是： ASCII （預設值） 或國際標準。|若要以動態方式設定這個選項，使用**COLLATINGSEQUENCE**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|資料來源名稱|識別資料來源，例如，薪資或人員的名稱。|若要以動態方式設定這個選項，使用**DSN**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|資料庫|Microsoft Access 資料來源可以設定而不需要選取或建立資料庫。 如果資料庫不提供在安裝程式時，會提示使用者在連線至資料來源時選取的資料庫檔案。|若要以動態方式設定這個選項，使用**DBQ**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|Description|選擇性的描述資料來源; 中的資料例如，"雇用日期、 薪資記錄以及目前檢視的所有員工。 」|若要以動態方式設定這個選項，使用**描述**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|排除|如果**獨佔**方塊已選取，資料庫會以獨佔模式開啟，並只有一位使用者可以存取一次。 獨佔模式中執行時，會增強效能。|若要以動態方式設定這個選項，使用**獨佔**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|頁面逾時|指定一段時間中的十分之一秒、 的頁面 （如果不使用） 會在緩衝區中保留多久然後才移除。 預設值為 600 的十分之一秒 （60 秒）。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 由於固有的延遲，頁面逾時不能為 0。 頁面逾時不能早於固有的延遲，即使頁面逾時選項設定低於的值。|若要以動態方式設定這個選項，使用**PAGETIMEOUT**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定這個選項，使用**READONLY**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取之的檔案的目錄。<br /><br /> 當您定義資料來源目錄時，指定您最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果經常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式中的檔案名稱以目錄名稱：<br /><br /> 選取\*C:\MYDIR\EMP 從<br /><br /> 或者，您可以指定新的預設目錄使用**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項具有函式。|若要以動態方式設定這個選項，使用**DEFAULTDIR**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|顯示刪除的資料列|指定是否可以擷取或位於已標示為已刪除的資料列。 如果清除，不會顯示刪除的資料列。如果選取，已刪除資料列會被視為未刪除的資料列相同。 預設值為清除此核取方塊。|若要以動態方式設定這個選項，使用**刪除**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|

