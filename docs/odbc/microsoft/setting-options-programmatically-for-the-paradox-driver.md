---
title: 設定以程式設計方式 Paradox 驅動程式的選項 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fa8084499f38a7152eb5eeab50010b919f4a06e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以程式設計的方式 Paradox 驅動程式的設定選項
|選項|Description|方法|  
|------------|-----------------|------------|  
|目錄|設定的目標的目錄。|若要以動態方式設定這個選項，使用**DEFAULTDIR**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|定序順序|欄位排序順序。<br /><br /> 序列可以是 ASCII （預設值）、 國際、 瑞典文-芬蘭文或挪威文丹麥文。|若要以動態方式設定這個選項，使用**COLLATINGSEQUENCE**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|Description|選擇性的描述資料來源; 中的資料例如，"雇用日期、 薪資記錄以及目前檢視的所有員工。 」|若要以動態方式設定這個選項，使用**描述**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|排除|如果**獨佔**方塊已選取，資料庫會以獨佔模式開啟，並只有一位使用者可以存取一次。 以獨佔模式執行時，會增強效能。|若要以動態方式設定這個選項，使用**獨佔**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|Net 樣式|若要存取 Paradox 資料時使用的網路存取樣式： 任一"3。*x*"Paradox 3。*x*或"4。*x*」 的 Paradox 4。*x*或 5。*x*。 可以設定為"3。*x*"或"4。*x*"Paradox 4 版本時。*x*或 5。*x*; 如果版本是 Paradox 3。*x*，樣式必須是"3。*x*"。|若要以動態方式設定這個選項，使用**PARADOXNETSTYLE**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|頁面逾時|指定一段時間中的每秒，被移除之前頁面 （如果不使用） 會保留在緩衝區中的十分之一。 預設值為 600 的十分之一秒 （60 秒）。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 由於固有的延遲，頁面逾時不能為 0。 頁面逾時不能早於固有的延遲，即使頁面逾時選項設定低於的值。|若要以動態方式設定這個選項，使用**PAGETIMEOUT**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定這個選項，使用**READONLY**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取的檔案的目錄。<br /><br /> 當定義資料來源目錄指定的目錄，您最常使用的檔案的位置。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果經常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式中的檔案名稱以目錄名稱：<br /><br /> 選取\*C:\MYDIR\EMP 從<br /><br /> 或者，您可以指定新的預設目錄使用**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項具有函式。|若要以動態方式設定這個選項，使用**DEFAULTDIR**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|選取網路目錄|包含 Paradox 鎖定資料庫，因為它包含 Pdoxusrs.net 檔案的目錄的完整路徑 (在 Paradox 4。*x*) 或 Paradox.net 檔案 (Paradox 5。*x*)。 如果目錄不包含這些檔案，Paradox 驅動程式會建立一個。 如需這些檔案的資訊，請參閱 Paradox 文件。<br /><br /> 您可以選取網路目錄之前，您必須輸入 Paradox 的使用者名稱**使用者名**文字方塊。 按一下**選取網路目錄**選取網路目錄。|若要以動態方式設定這個選項，使用**PARADOXNETPATH**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|  
|使用者名稱|Paradox 使用者名稱。 這是在發生鎖定時，顯示 Paradox 檔案的其他使用者的名稱。|若要以動態方式設定這個選項，使用**PARADOXUSERNAME**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。|
