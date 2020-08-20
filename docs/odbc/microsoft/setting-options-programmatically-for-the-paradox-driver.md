---
description: 以程式設計方式設定 Paradox 驅動程式的選項
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 85b63df9e18b835c96bc0e59f7c937ece69f3999
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471570"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>以程式設計方式設定 Paradox 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|目錄|設定目標目錄。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|排序次序|欄位的排序次序。<br /><br /> 順序可以是預設) 、國際、瑞典文或挪威文（丹麥文） (的 ASCII。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**COLLATINGSEQUENCE**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄和目前的員工評論」。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|獨佔|如果選取 [ **獨佔** ] 方塊，資料庫將會在獨佔模式中開啟，而且一次只能由一個使用者存取。 在獨佔模式中執行時，效能會增強。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**EXCLUSIVE**關鍵字。|  
|Net 樣式|存取 Paradox 資料時要使用的網路存取樣式：「3.*x*」代表 paradox 3。*x* 或 "4。*x*"代表 Paradox 4。*x* 或5。*x*。 可以設定為 "3。*x*"或" 4。*x*"如果版本為 Paradox 4。*x* 或5。*x*;如果版本為 Paradox 3。*x*，樣式必須是 "3。*x*」。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PARADOXNETSTYLE**關鍵字。|  
|頁面超時|指定一段時間（以十分之一秒為限），頁面 (（如果未使用）) 會在移除之前保留在緩衝區中。 預設值為600十分之一秒 (60 秒) 。 此選項適用于所有使用 ODBC 驅動程式的資料來源。<br /><br /> 頁面超時不可以是0，因為有固有的延遲。 即使 page timeout 選項設定為低於該值，頁面的超時時間也不能小於固有的延遲。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|選取目錄|顯示對話方塊，您可以在其中選取包含要存取之檔案的目錄。<br /><br /> 定義資料來源目錄時，請指定您最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄作為預設目錄。 如果經常使用檔案，請將其他檔案複製到此目錄。 或者，您可以在 SELECT 語句中使用目錄名稱來限定檔案名：<br /><br /> \*從 C:\MYDIR\EMP 中選取<br /><br /> 或者，您可以使用 **SQLSetConnectOption** 函數搭配 SQL_CURRENT_QUALIFIER 選項，以指定新的預設目錄。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|選取網路目錄|包含 Paradox 鎖定資料庫之目錄的完整路徑，因為它包含 Pdoxusrs.net 檔 (的 Paradox 4。*x*) 或 Paradox.net 檔案 (的 Paradox 為5。*x*) 。 如果目錄不包含這些檔案的其中一個，Paradox 驅動程式會建立一個。 如需這些檔案的詳細資訊，請參閱 Paradox 檔。<br /><br /> 您必須在 [ **使用者名稱** ] 文字方塊中輸入 Paradox 的使用者名稱，才能選取網路目錄。 按一下 [ **選取網路目錄** ] 以選取網路目錄。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PARADOXNETPATH**關鍵字。|  
|使用者名稱|Paradox 的使用者名稱。 這是遇到鎖定時，對其他 Paradox 檔案的使用者所顯示的名稱。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)的呼叫中使用**PARADOXUSERNAME**關鍵字。|
