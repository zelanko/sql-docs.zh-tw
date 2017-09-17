---
title: "設定 Excel 驅動程式以程式設計方式的選項 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da1f2ed6bbca3709c8223713f4841ed34288f5a3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>設定 Excel 驅動程式以程式設計方式的選項
|選項|Description|方法|  
|------------|-----------------|------------|  
|資料來源名稱|識別資料來源，例如，薪資或人員的名稱。|若要以動態方式設定這個選項，使用**DSN**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|資料庫|Microsoft Access 資料來源可以設定而不需要選取或建立資料庫。 如果資料庫不提供在安裝程式時，您就會提示使用者選擇連接到資料來源時的資料庫檔案。|若要以動態方式設定這個選項，使用**DBQ**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|Description|選擇性的描述資料來源; 中的資料例如，"雇用日期、 薪資記錄以及目前檢視的所有員工。 」|若要以動態方式設定這個選項，使用**描述**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|目錄|顯示目前所選取的目錄。<br /><br /> Microsoft Excel 3.0/4.0 檔案的路徑顯示標示為 「 目錄 」，如 Microsoft Excel 5.0 版，而 7.0，或 97 檔案的路徑顯示標示為 「 活頁簿 」。|若要以動態方式設定這個選項，使用**DEFAULTDIR**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定這個選項，使用**READONLY**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|要掃描的資料列|若要掃描以判斷每個資料行的資料類型的資料列數目。 找到的資料類型的最大值來決定的資料類型。 如果遇到猜測資料行資料類型不符的資料，資料類型會傳回為 NULL 值。<br /><br /> Microsoft Excel 驅動程式，您可以輸入的數字 1 到 16 個要掃描的資料列。 預設值為 8。如果設定為 0，會掃描所有資料列。 （限制以外的數字會傳回錯誤）。|若要以動態方式設定這個選項，使用**於 MAXSCANROWS**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取的檔案的目錄。<br /><br /> 在定義資料來源目錄 （適用於 Microsoft Access 以外的所有驅動程式） 時，指定您最常使用的檔案所在的目錄。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果經常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式中的檔案名稱以目錄名稱：<br /><br /> 選取\*C:\MYDIR\EMP 從<br /><br /> 或者，您可以指定新的預設目錄使用**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項具有函式。<br /><br /> Microsoft Excel 3.0 或 4.0 版的檔案，路徑顯示標示為 「 目錄 」，而且路徑的 [選取範圍] 按鈕會標示為 「 選取目錄 」。 5.0、 7.0、 或 97 Microsoft Excel 檔案路徑顯示標示為 「 活頁簿 」 和 「 路徑 」 選取範圍按鈕會標示為 「 選取活頁簿 」。 在定義資料來源目錄時，指定最常使用的 Microsoft Excel 檔案所在的 Microsoft Excel 3.0/4.0、 目錄或位於 5.0、 7.0、 或 97 Microsoft excel 活頁簿檔案所在的目錄。 **使用目前的目錄**已停用 Microsoft Excel 5.0、 7.0 和 97。|若要以動態方式設定這個選項，使用**DEFAULTDIR**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。|
