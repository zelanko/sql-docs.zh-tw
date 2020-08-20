---
description: 以程式設計方式設定 dBASE 驅動程式的選項
title: 以程式設計方式設定 dBASE 驅動程式的選項 |Microsoft Docs
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
ms.openlocfilehash: 7c4b86b8284ca9a47e3ad40b1680a362035a3f13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471580"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>以程式設計方式設定 dBASE 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|大約資料列計數|判斷資料表大小統計資料是否近似。 此選項適用于所有使用 ODBC 驅動程式的資料來源。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**STATISTICS**關鍵字。|  
|排序次序|欄位的排序次序。<br /><br /> 順序可以是： ASCII (預設) 或國際。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**COLLATINGSEQUENCE**關鍵字。|  
|資料來源名稱|識別資料來源的名稱，例如薪資或人員。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DSN**關鍵字。|  
|資料庫|您可以設定 Microsoft Access 資料來源，而不需選取或建立資料庫。 如果在安裝時未提供任何資料庫，當使用者連接到資料來源時，系統會提示使用者選取資料庫檔案。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DBQ**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄和目前的員工評論」。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|獨佔|如果選取 [ **獨佔** ] 方塊，資料庫將會在獨佔模式中開啟，而且一次只能由一個使用者存取。 當效能在獨佔模式中執行時，會增強效能。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**EXCLUSIVE**關鍵字。|  
|頁面超時|指定一段時間（以十分之一秒為限），頁面 (（如果未使用）) 會在移除之前保留在緩衝區中。 預設值為600十分之一秒 (60 秒) 。 此選項適用于所有使用 ODBC 驅動程式的資料來源。<br /><br /> 頁面超時不可以是0，因為有固有的延遲。 即使 page timeout 選項設定為低於該值，頁面的超時時間也不能小於固有的延遲。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**PAGETIMEOUT**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|選取目錄|顯示對話方塊，您可以在其中選取包含要存取之檔案的目錄。<br /><br /> 當您定義資料來源目錄時，請指定最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄作為預設目錄。 如果經常使用檔案，請將其他檔案複製到此目錄。 或者，您可以在 SELECT 語句中使用目錄名稱來限定檔案名：<br /><br /> \*從 C:\MYDIR\EMP 中選取<br /><br /> 或者，您可以使用 **SQLSetConnectOption** 函數搭配 SQL_CURRENT_QUALIFIER 選項，以指定新的預設目錄。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|顯示已刪除的資料列|指定是否可以取出或定位已標示為已刪除的資料列。 如果已清除，則不會顯示已刪除的資料列;若選取此選項，則會將已刪除的資料列視為與未刪除的資料列相同。 預設值為清除此核取方塊。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)的呼叫中使用**DELETED**關鍵字。|
