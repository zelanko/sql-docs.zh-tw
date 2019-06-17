---
title: 設定 Paradox 驅動程式以程式設計方式的選項 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd92344552371e2e052a958485340b70522cc121
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313564"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以程式設計方式設定 Paradox 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|目錄|設定的目標的目錄。|若要以動態方式設定此選項，請使用**DEFAULTDIR**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|定序順序|欄位會排序順序。<br /><br /> 序列可以是 ASCII （預設值）、 國際、 瑞典文-芬蘭文或挪威文-丹麥文。|若要以動態方式設定此選項，請使用**COLLATINGSEQUENCE**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|描述|資料來源中資料的選擇性描述比方說，「 雇用日期、 薪資記錄以及目前檢閱所有員工。 」|若要以動態方式設定此選項，請使用**描述**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|排除|如果**獨佔**方塊已選取，資料庫會以獨佔模式開啟，並只有一位使用者可以存取一次。 以獨佔模式執行時，會增強效能。|若要以動態方式設定此選項，請使用**獨佔**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|Net 的樣式|若要存取 Paradox 資料時使用的網路存取樣式： 任一"3。*x*"Paradox 3。*x*或 「 4。*x*"Paradox 4 的。*x*或 5。*x*。 可以設定為"3。*x*"或"4。*x*"Paradox 4 版本時。*x*或 5。*x*; 如果版本為 Paradox 3。*x*，樣式必須是 「 3。*x*"。|若要以動態方式設定此選項，請使用**PARADOXNETSTYLE**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|頁面逾時|指定的時間，以第二個方法，移除前頁面 （如果未使用） 會保留在緩衝區中的十分之一。 預設值為 600 的十分之一秒 （60 秒）。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 在頁面上的逾時不能為 0，由於固有的延遲。 在頁面上的逾時不能早於固有的延遲，即使頁面的 [逾時] 選項設定的值如下。|若要以動態方式設定此選項，請使用**PAGETIMEOUT**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定此選項，請使用**READONLY**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取的檔案的目錄。<br /><br /> 當定義資料來源目錄指定的目錄，您最常使用的檔案的位置。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果較常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式與目錄名稱的檔案名稱：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，您可以藉由指定新的預設目錄**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項的函式。|若要以動態方式設定此選項，請使用**DEFAULTDIR**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|選取網路目錄|包含 Paradox 鎖定資料庫，因為它包含 Pdoxusrs.net 檔案的目錄的完整路徑 (Paradox 4。*x*) 或 Paradox.net 檔案 (Paradox 5。*x*)。 如果目錄不包含其中一個檔案，Paradox 驅動程式會建立一個。 如需這些檔案的詳細資訊，請參閱 Paradox 文件。<br /><br /> 您可以選取網路目錄之前，您必須輸入 Paradox 的使用者名稱**使用者名**文字方塊。 按一下 **選取 網路目錄**選取網路目錄。|若要以動態方式設定此選項，請使用**PARADOXNETPATH**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|使用者名稱|Paradox 的使用者名稱。 這是在遇到鎖定時顯示 Paradox 檔案的其他使用者的名稱。|若要以動態方式設定此選項，請使用**PARADOXUSERNAME**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|
