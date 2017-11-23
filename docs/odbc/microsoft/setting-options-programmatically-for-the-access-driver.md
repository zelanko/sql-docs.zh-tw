---
title: "設定以程式設計方式存取驅動程式的選項 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed08d24f96b66b69bbff409cbc2c9e203526041b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以程式設計的方式存取驅動程式的設定選項
|選項|Description|方法|  
|------------|-----------------|------------|  
|緩衝區大小|內部緩衝區大小，以 kb 為單位，Microsoft Access 所用來傳輸資料磁碟。 預設緩衝區大小是 2048 KB （顯示為 2048年）。 您可以輸入任何 256 整除的整數值。|若要以動態方式設定這個選項，使用的 MAXBUFFERSIZE 關鍵字的呼叫中[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|資料來源名稱|識別資料來源，例如，薪資或人員的名稱。|若要以動態方式設定這個選項，使用**DSN**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|資料庫|Microsoft Access 資料來源可以設定而不需要選取或建立資料庫。 如果資料庫不提供在安裝程式時，您就會提示使用者選擇連接到資料來源時的資料庫檔案。|若要以動態方式設定這個選項，使用**DBQ**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|Description|選擇性的描述資料來源; 中的資料例如，"雇用日期、 薪資記錄以及目前檢視的所有員工。 」|若要以動態方式設定這個選項，使用**描述**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|排除|如果**獨佔**方塊已選取，資料庫會以獨佔模式開啟，並只有一位使用者可以存取一次。 以獨佔模式執行時，會增強效能。|若要以動態方式設定這個選項，使用**獨佔**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|ImplicitCommitSync|決定如何在交易外所做的變更會寫入資料庫。 這個值最初是設定為"Yes"，這表示 Microsoft Access 驅動程式將等候中的內部/隱含的交易完成認可。|此選項會包含在**設定進階選項**Microsoft Access 驅動程式 對話方塊。|  
|頁面逾時|指定一段時間，以毫秒為單位，移除之前頁面 （如果不使用） 會保留在緩衝區中。 Microsoft Access 驅動程式時，預設值是 500 毫秒 （0.5 秒為單位）。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 由於固有的延遲，頁面逾時不能為 0。 頁面逾時不能早於固有的延遲，即使頁面逾時選項設定低於的值。|若要以動態方式設定這個選項，使用**PAGETIMEOUT**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定這個選項，使用**READONLY**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|系統資料庫|Microsoft Access 系統資料庫，以用於您想要存取 Microsoft Access 資料庫的完整路徑。<br /><br /> 按一下**系統資料庫**按鈕來選取要使用的系統資料庫。 ODBC Microsoft Access 驅動程式會提示使用者輸入的名稱和密碼。 預設名稱是系統管理員和系統管理員使用者的 Microsoft Access 中的預設密碼為空字串。<br /><br /> 若要增加您的 Microsoft Access 資料庫的安全性，請建立新的使用者，以取代系統管理使用者，並刪除系統管理員的使用者，或變更系統管理使用者可存取的物件。|若要以動態方式設定這個選項，使用**SYSTEMDB**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|Threads|引擎使用的背景執行緒數目。 Microsoft Access 驅動程式，這個值會預設為 3，但可以變更。 使用者可能想要增加的執行緒數目，如果有大量的資料庫中的活動。<br /><br /> 此選項會包含在**設定進階選項**Microsoft Access 驅動程式 對話方塊。|若要以動態方式設定這個選項，使用**執行緒**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|UserCommitSync|決定是否 Microsoft Access 驅動程式將執行明確的使用者定義交易以非同步的方式。 這個值最初是設定為"Yes"，這表示 Microsoft Access 驅動程式會等候之使用者定義的交易完成認可。<br /><br /> 將此選項設定為 False，可以在多使用者環境中有無法預期的結果。|若要以動態方式設定這個選項，使用**USERCOMMITSYNC**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|
