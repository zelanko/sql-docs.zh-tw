---
title: 以程式設計方式設定 Paradox 驅動程式的選項 |Microsoft Docs
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
ms.openlocfilehash: 658d03469e2733b0c25513a4d4a89c6ab88b9852
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063508"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以程式設計方式設定 Paradox 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|Directory|設定目標目錄。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|排序次序|排序欄位的順序。<br /><br /> 此順序可以是 ASCII （預設值）、國際、瑞典文-芬蘭文或挪威文-丹麥文。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**COLLATINGSEQUENCE**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄，以及所有員工的目前評論」。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|獨佔|如果選取 [**獨佔**] 方塊，資料庫將會以獨佔模式開啟，而且一次只能由一個使用者存取。 在獨佔模式中執行時，效能會增強。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**EXCLUSIVE**關鍵字。|  
|Net 樣式|存取 Paradox 資料時要使用的網路存取樣式： "3.*x*" 代表 paradox 3。*x*或 "4。*x*"代表 Paradox 4。*x*或5。*x*。 可以設定為 "3。*x*"或" 4。*x*"（如果版本是 Paradox 4）。*x*或5。*x*;如果版本是 Paradox 3，則為。*x*，樣式必須是 "3。*x*"。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PARADOXNETSTYLE**關鍵字。|  
|頁面超時|指定在移除之前，頁面（如果未使用）會保留在緩衝區中的一段時間，以十分之一秒為限。 預設值為600十分之一秒（60秒）。 此選項適用于使用 ODBC 驅動程式的所有資料來源。<br /><br /> 頁面超時不可以是0，因為有固有的延遲。 頁面超時不能小於固有的延遲，即使 page timeout 選項設為低於該值也一樣。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|選取目錄|顯示對話方塊，您可以在其中選取目錄，其中包含您想要存取的檔案。<br /><br /> 定義資料來源目錄時，請指定最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄做為預設目錄。 如果經常使用檔案，請將其他檔案複製到這個目錄中。 或者，您也可以在 SELECT 語句中，使用目錄名稱來限定檔案名：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，您可以使用**SQLSetConnectOption**函數搭配 SQL_CURRENT_QUALIFIER 選項來指定新的預設目錄。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|選取網路目錄|包含 Paradox 鎖定資料庫之目錄的完整路徑，因為它包含 Pdoxusrs.net 檔案（在 Paradox 4 中）。*x*）或 Paradox.net 檔案（在 Paradox 5 中。*x*）。 如果目錄不包含這些檔案的其中一個，則 Paradox 驅動程式會建立一個。 如需這些檔案的詳細資訊，請參閱 Paradox 檔。<br /><br /> 在您可以選取網路目錄之前，您必須在 [**使用者名稱**] 文字方塊中輸入您的 Paradox 使用者名稱。 按一下 [**選取網路目錄**] 以選取網路目錄。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PARADOXNETPATH**關鍵字。|  
|使用者名稱|Paradox 的使用者名稱。 這是當遇到鎖定時，會向其他 Paradox 檔案的使用者顯示的名稱。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PARADOXUSERNAME**關鍵字。|
