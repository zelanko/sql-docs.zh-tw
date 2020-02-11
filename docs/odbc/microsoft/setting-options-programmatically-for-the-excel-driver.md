---
title: 針對 Excel 驅動程式以程式設計方式設定選項 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 47181fca07aff7b2a0d418b8852cfce47cf9e501
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063517"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以程式設計方式設定 Excel 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|資料來源名稱|識別資料來源的名稱，例如薪資或人員。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DSN**關鍵字。|  
|資料庫|您可以設定 Microsoft Access 資料來源，而不需要選取或建立資料庫。 如果在安裝時未提供任何資料庫，則在連接到資料來源時，系統會提示使用者選擇資料庫檔案。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DBQ**關鍵字。|  
|描述|資料來源中資料的選擇性描述;例如，「雇用日期、薪資歷程記錄，以及所有員工的目前評論」。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DESCRIPTION**關鍵字。|  
|Directory|顯示目前選取的目錄。<br /><br /> 針對 Microsoft Excel 3.0/4.0 檔案，路徑顯示標示為「目錄」，而在 Microsoft Excel 5.0、7.0 或97檔案中，路徑顯示標示為「活頁簿」。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|  
|唯讀|將資料庫指定為唯讀。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**READONLY**關鍵字。|  
|要掃描的資料列|要掃描的資料列數目，以判斷每個資料行的資料類型。 資料類型是根據找到的最大資料種類數目而決定。 如果遇到的資料與資料行猜測的資料類型不相符，資料類型將會以 Null 值傳回。<br /><br /> 針對 Microsoft Excel 驅動程式，您可以輸入1到16的數位，以供要掃描的資料列使用。 值預設為 8;如果設定為0，則會掃描所有資料列。 （超出限制的數位將會傳回錯誤）。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**MAXSCANROWS**關鍵字。|  
|選取目錄|顯示對話方塊，您可以在其中選取目錄，其中包含您想要存取的檔案。<br /><br /> 定義資料來源目錄（適用于 Microsoft Access 以外的所有驅動程式）時，請指定最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄做為預設目錄。 如果經常使用檔案，請將其他檔案複製到這個目錄中。 或者，您也可以在 SELECT 語句中，使用目錄名稱來限定檔案名：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，您可以使用**SQLSetConnectOption**函數搭配 SQL_CURRENT_QUALIFIER 選項來指定新的預設目錄。<br /><br /> 若為 Microsoft Excel 3.0 或4.0 檔案，路徑顯示會標示為「目錄」，而路徑選取按鈕則會標示為「選取目錄」。 針對 Microsoft Excel 5.0、7.0 或97檔案，路徑顯示標示為「活頁簿」，而路徑選取按鈕則標示為「選取活頁簿」。 定義資料來源目錄時，請指定最常使用的 Microsoft Excel 檔案在 Microsoft Excel 3.0/4.0 中的所在目錄，或是活頁簿檔案所在的目錄（適用于 Microsoft Excel 5.0、7.0 或97）。 已停用 Microsoft Excel 5.0、7.0 和97的 [**使用目前目錄**]。|若要動態設定此選項，請在[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)的呼叫中使用**DEFAULTDIR**關鍵字。|
