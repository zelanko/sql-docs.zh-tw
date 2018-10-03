---
title: 設定以程式設計方式存取驅動程式的選項 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5227985c56d5e2fd4730c86fe9182c8b16b2cb02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804456"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>以程式設計方式設定 Access 驅動程式的選項
|選項|描述|方法|  
|------------|-----------------|------------|  
|緩衝區大小|內部緩衝區大小，以 kb 為單位，Microsoft Access 所用來傳輸資料進出磁碟。 預設緩衝區大小為 2048 KB （顯示為 2048年）。 您可以輸入任何以 256 整除的整數值。|若要以動態方式設定此選項，請在呼叫中使用 MAXBUFFERSIZE 關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|資料來源名稱|識別資料來源，例如薪資或人員的名稱。|若要以動態方式設定此選項，請使用**DSN**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|[資料庫]|Microsoft Access 資料來源可以設定而不需要選取或建立資料庫。 如果未提供資料庫安裝程式時，您就會提示使用者連接到資料來源時，請選擇資料庫檔案。|若要以動態方式設定此選項，請使用**DBQ**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|描述|資料來源中資料的選擇性描述比方說，「 雇用日期、 薪資記錄以及目前檢閱所有員工。 」|若要以動態方式設定此選項，請使用**描述**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|排除|如果**獨佔**方塊已選取，資料庫會以獨佔模式開啟，並只有一位使用者可以存取一次。 以獨佔模式執行時，會增強效能。|若要以動態方式設定此選項，請使用**獨佔**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|ImplicitCommitSync|決定如何在交易外所做的變更會寫入資料庫。 此值一開始是設定為 [是]，這表示 Microsoft Access 驅動程式會等待完成內部/隱含交易中認可。|此選項會納入**設定進階選項**Microsoft Access 驅動程式 對話方塊。|  
|頁面逾時|指定的時間週期，以毫秒為單位，移除前頁面 （如果未使用） 會保留在緩衝區中。 Microsoft Access 驅動程式時，預設值是 500 毫秒 （0.5 秒為單位）。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 在頁面上的逾時不能為 0，由於固有的延遲。 在頁面上的逾時不能早於固有的延遲，即使頁面的 [逾時] 選項設定的值如下。|若要以動態方式設定此選項，請使用**PAGETIMEOUT**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定此選項，請使用**READONLY**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|系統資料庫|您想要存取搭配 Microsoft Access 資料庫的 Microsoft Access 系統資料庫的完整路徑。<br /><br /> 按一下 **系統資料庫**按鈕來選取要使用的系統資料庫。 ODBC Microsoft Access 驅動程式會提示使用者輸入的名稱和密碼。 預設名稱是系統管理員，並在 Microsoft Access 中的系統管理使用者的預設密碼為空字串。<br /><br /> 若要增加您的 Microsoft Access 資料庫的安全性，請建立新的使用者，以取代的系統管理使用者，並刪除系統管理員的使用者，或變更的系統管理使用者有權存取的物件。|若要以動態方式設定此選項，請使用**SYSTEMDB**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|Threads|引擎使用的背景執行緒數目。 Microsoft Access 驅動程式，這個值預設值為 3，但可以變更。 使用者可能想要增加的執行緒數目，如果有大量的資料庫中的活動。<br /><br /> 此選項會納入**設定進階選項**Microsoft Access 驅動程式 對話方塊。|若要以動態方式設定此選項，請使用**執行緒**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|  
|UserCommitSync|判斷是否 Microsoft Access 驅動程式會執行明確的使用者定義交易以非同步的方式。 此值一開始是設定為 [是]，這表示 Microsoft Access 驅動程式將等候中的使用者定義的交易完成認可。<br /><br /> 將此選項設定為 False，可以在多使用者環境中有無法預期的結果。|若要以動態方式設定此選項，請使用**USERCOMMITSYNC**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。|
