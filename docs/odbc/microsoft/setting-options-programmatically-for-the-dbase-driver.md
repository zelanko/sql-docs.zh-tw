---
title: 選項以程式設計方式設定 dbase 驅動程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a268e72262f9f8252ea89774876f3d04008fe4c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63284950"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以程式設計方式設定 dBASE 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|大約的資料列計數|決定是否接近資料表大小統計資料。 此選項適用於使用 ODBC 驅動程式的所有資料來源。|若要以動態方式設定此選項，請使用**統計資料**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|定序順序|欄位會排序順序。<br /><br /> 序列可以是：ASCII （預設值） 或國際。|若要以動態方式設定此選項，請使用**COLLATINGSEQUENCE**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|資料來源名稱|識別資料來源，例如薪資或人員的名稱。|若要以動態方式設定此選項，請使用**DSN**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|[資料庫]|Microsoft Access 資料來源可以設定而不需要選取或建立資料庫。 如果未提供資料庫安裝程式時，您就會提示使用者在連線到資料來源時，請選取資料庫檔案。|若要以動態方式設定此選項，請使用**DBQ**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|描述|資料來源中資料的選擇性描述比方說，「 雇用日期、 薪資記錄以及目前檢閱所有員工。 」|若要以動態方式設定此選項，請使用**描述**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|排除|如果**獨佔**方塊已選取，資料庫會以獨佔模式開啟，並只有一位使用者可以存取一次。 以獨佔模式執行時，會增強效能。|若要以動態方式設定此選項，請使用**獨佔**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|頁面逾時|中的十分之一秒、 頁面 （如果未使用） 會保留在緩衝區中，在移除之前，指定一段時間。 預設值為 600 的十分之一秒 （60 秒）。 此選項適用於使用 ODBC 驅動程式的所有資料來源。<br /><br /> 在頁面上的逾時不能為 0，由於固有的延遲。 在頁面上的逾時不能早於固有的延遲，即使頁面的 [逾時] 選項設定的值如下。|若要以動態方式設定此選項，請使用**PAGETIMEOUT**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定此選項，請使用**READONLY**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取之的檔案的目錄。<br /><br /> 當您定義資料來源目錄時，指定您最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果較常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式與目錄名稱的檔案名稱：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，您可以藉由指定新的預設目錄**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項的函式。|若要以動態方式設定此選項，請使用**DEFAULTDIR**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|  
|顯示已刪除的資料列|指定是否可以擷取或位於已標示為已刪除的資料列。 如果清除，不會顯示已刪除的資料列;如果選取，已刪除的資料列會視為非刪除資料列相同。 預設值為清除此核取方塊。|若要以動態方式設定此選項，請使用**DELETED**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。|
