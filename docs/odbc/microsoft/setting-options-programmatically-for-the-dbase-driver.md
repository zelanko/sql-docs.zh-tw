---
title: 針對 dBASE 驅動程式以程式設計方式設定選項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75889d9ff3ccfe01f9b8d5141df7774205522815
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300778"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以程式設計方式設定 dBASE 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|大約的資料列計數|判斷資料表大小統計資料是否近似。 此選項適用于使用 ODBC 驅動程式的所有資料來源。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**STATISTICS**關鍵字。|  
|排序次序|排序欄位的順序。<br /><br /> 順序可以是： ASCII （預設值）或國際。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**COLLATINGSEQUENCE**關鍵字。|  
|資料來源名稱|識別資料來源的名稱，例如薪資或人員。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DSN**關鍵字。|  
|資料庫|您可以設定 Microsoft Access 資料來源，而不需要選取或建立資料庫。 如果在安裝時未提供任何資料庫，當使用者連接到資料來源時，系統會提示他們選取資料庫檔案。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DBQ**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄，以及所有員工的目前評論」。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|獨佔|如果選取 [**獨佔**] 方塊，資料庫將會以獨佔模式開啟，而且一次只能由一個使用者存取。 在獨佔模式中執行時，效能會增強。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**EXCLUSIVE**關鍵字。|  
|頁面超時|指定在移除之前，頁面（如果未使用）保留在緩衝區中的一段時間（以十分之一秒為限）。 預設值為600十分之一秒（60秒）。 此選項適用于使用 ODBC 驅動程式的所有資料來源。<br /><br /> 頁面超時不可以是0，因為有固有的延遲。 頁面超時不能小於固有的延遲，即使 page timeout 選項設為低於該值也一樣。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|選取目錄|顯示對話方塊，您可以在其中選取目錄，其中包含您想要存取的檔案。<br /><br /> 當您定義資料來源目錄時，請指定最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄做為預設目錄。 如果經常使用檔案，請將其他檔案複製到這個目錄中。 或者，您也可以在 SELECT 語句中，使用目錄名稱來限定檔案名：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，您可以使用**SQLSetConnectOption**函數搭配 SQL_CURRENT_QUALIFIER 選項來指定新的預設目錄。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|顯示已刪除的資料列|指定是否可以抓取或定位已標示為已刪除的資料列。 如果清除此選項，則不會顯示已刪除的資料列;如果選取此選項，刪除的資料列就會被視為與非刪除的資料列相同。 預設值為清除此核取方塊。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DELETED**關鍵字。|
