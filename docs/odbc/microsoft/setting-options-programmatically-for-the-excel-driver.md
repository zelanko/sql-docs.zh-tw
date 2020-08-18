---
description: 以程式設計方式設定 Excel 驅動程式的選項
title: 以程式設計方式設定 Excel 驅動程式的選項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97a17a0967581f4097b5030adb803a69c6a82f80
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449250"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以程式設計方式設定 Excel 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|資料來源名稱|識別資料來源的名稱，例如薪資或人員。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DSN**關鍵字。|  
|資料庫|您可以設定 Microsoft Access 資料來源，而不需選取或建立資料庫。 如果在安裝時未提供任何資料庫，則在連接至資料來源時，系統會提示使用者選擇資料庫檔案。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DBQ**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄和目前的員工評論」。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|目錄|顯示目前選取的目錄。<br /><br /> 若為 Microsoft Excel 3.0/4.0 檔案，路徑顯示會標示為「目錄」，而針對 Microsoft Excel 5.0、7.0 或97檔案，路徑顯示會標示為「活頁簿」。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|要掃描的資料列|要掃描的資料列數目，以決定每個資料行的資料類型。 資料類型會根據找到的資料類型數目上限來決定。 如果遇到的資料與資料行猜測的資料類型不相符，則資料類型會以 Null 值傳回。<br /><br /> 若為 Microsoft Excel 驅動程式，您可以輸入從1到16的數位，以掃描資料列。 值預設為 8;如果設定為0，則會掃描所有資料列。  (超出限制的數位將會傳回錯誤。 ) |若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**MAXSCANROWS**關鍵字。|  
|選取目錄|顯示對話方塊，您可以在其中選取包含要存取之檔案的目錄。<br /><br /> 針對所有驅動程式（Microsoft Access) 除外）定義資料來源目錄 (時，請指定最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄作為預設目錄。 如果經常使用檔案，請將其他檔案複製到此目錄。 或者，您可以在 SELECT 語句中使用目錄名稱來限定檔案名：<br /><br /> \*從 C:\MYDIR\EMP 中選取<br /><br /> 或者，您可以使用 **SQLSetConnectOption** 函數搭配 SQL_CURRENT_QUALIFIER 選項，以指定新的預設目錄。<br /><br /> 若為 Microsoft Excel 3.0 或4.0 檔案，路徑顯示會標示為「目錄」，而直接選取按鈕會標示為「選取目錄」。 若為 Microsoft Excel 5.0、7.0 或97檔案，路徑顯示會標示為「活頁簿」，而直接選取按鈕會標示為「選取活頁簿」。 定義資料來源目錄時，請指定您最常使用的 Microsoft Excel 檔案所在的目錄（適用于 Microsoft Excel 3.0/4.0），或是活頁簿檔案所在的目錄（適用于 Microsoft Excel 5.0、7.0 或97）。 Microsoft Excel 5.0、7.0 和97已停**用 [使用目前的目錄**]。|若要動態設定這個選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|
