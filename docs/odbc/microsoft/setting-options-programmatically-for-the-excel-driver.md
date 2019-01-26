---
title: 設定 Excel 驅動程式以程式設計方式的選項 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 271f61247b6083abd31657fe319bce234bc16f50
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044335"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>以程式設計方式設定 Excel 驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|資料來源名稱|識別資料來源，例如薪資或人員的名稱。|若要以動態方式設定此選項，請使用**DSN**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|[資料庫]|Microsoft Access 資料來源可以設定而不需要選取或建立資料庫。 如果未提供資料庫安裝程式時，您就會提示使用者連接到資料來源時，請選擇資料庫檔案。|若要以動態方式設定此選項，請使用**DBQ**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|描述|資料來源中資料的選擇性描述比方說，「 雇用日期、 薪資記錄以及目前檢閱所有員工。 」|若要以動態方式設定此選項，請使用**描述**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|目錄|顯示目前選取的目錄。<br /><br /> Microsoft Excel 3.0/4.0 檔案的路徑顯示標示為 「 目錄 」，如 Microsoft Excel 5.0 版，而 7.0，或 97 檔案的路徑顯示標示為 「 活頁簿 」。|若要以動態方式設定此選項，請使用**DEFAULTDIR**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定此選項，請使用**READONLY**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|要掃描的資料列|掃描以判斷每個資料行的資料類型的資料列數目。 指定找到的資料類型的最大數目來決定的資料類型。 如果發生資料不符合猜對的資料行的資料類型，將傳回的資料類型，為 NULL 值。<br /><br /> Microsoft Excel 驅動程式，您可以輸入的數字 1 到 16 個要掃描的資料列。 預設值為 8。如果它設定為 0，則會掃描所有資料列。 （限制以外的數字會傳回錯誤）。|若要以動態方式設定此選項，請使用**於 MAXSCANROWS**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取的檔案的目錄。<br /><br /> 在定義資料來源目錄 （適用於 Microsoft 存取以外的所有驅動程式） 時，指定您最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果較常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式與目錄名稱的檔案名稱：<br /><br /> SELECT \* FROM C:\MYDIR\EMP<br /><br /> 或者，您可以藉由指定新的預設目錄**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項的函式。<br /><br /> Microsoft Excel 3.0 或 4.0 版的檔案，路徑顯示標示為 「 目錄 」，而且路徑的選取範圍 按鈕會標示為 「 選取的目錄 」。 5.0、 7.0、 或 97 的 Microsoft Excel 檔案的路徑顯示標示為 「 活頁簿 」 並路徑選擇按鈕標示為 「 選取活頁簿 」。 在定義資料來源目錄時，指定您最常使用的 Microsoft Excel 檔案所在的 Microsoft Excel 3.0/4.0 中，目錄或 Microsoft Excel 5.0、 7.0、 或 97 到活頁簿檔案的目錄。 **使用目前的目錄**已停用適用於 Microsoft Excel 5.0、 7.0 和 97。|若要以動態方式設定此選項，請使用**DEFAULTDIR**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|
