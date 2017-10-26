---
title: "設定選項的文字檔案驅動程式以程式設計的方式 |Microsoft 文件"
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
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5037ca7d41470a2e9f7ce342ab49b08a6af0d74
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>設定文字檔案驅動程式以程式設計方式的選項
|選項|Description|方法|  
|------------|-----------------|------------|  
|資料來源名稱|識別資料來源，例如，薪資或人員的名稱。|若要以動態方式設定這個選項，使用**DSN**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|定義格式|顯示**定義文字格式** 對話方塊，並讓您指定資料來源目錄中的個別資料表的結構描述。|無法以動態方式設定這個選項，藉由呼叫[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|Description|選擇性的描述資料來源; 中的資料例如，"雇用日期、 薪資記錄以及目前檢視的所有員工。 」|若要以動態方式設定這個選項，使用**描述**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|目錄|選取的目標的目錄。|若要以動態方式設定這個選項，使用**DEFAULTDIR**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|擴充功能清單|列出的資料來源上的文字檔案的副檔名。 使用文字驅動程式時，沒有副檔名的名稱與執行 CREATE TABLE 陳述式時，會建立不含副檔名的檔案。 不提供任何擴充功能時，其他驅動程式會建立檔案與預設延伸模組。 若要建立副檔名為.txt 的檔案，就必須名稱中包含擴充功能。 若要顯示不含任何擴充功能檔案**定義文字格式**對話方塊中，"*。 」 必須加入至擴充功能清單。|若要以動態方式設定這個選項，使用**延伸**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定這個選項，使用**READONLY**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|要掃描的資料列|若要掃描以判斷每個資料行的資料類型的資料列數目。 找到的資料類型的最大值來決定的資料類型。 如果遇到猜測資料行資料類型不符的資料，資料類型會傳回為 NULL 值。<br /><br /> 文字驅動程式，您可能輸入的數字 1 到 32767 之間的掃描; 的資料列數目不過，值一律會預設為 25。 （限制以外的數字會傳回錯誤）。|若要以動態方式設定這個選項，使用**於 MAXSCANROWS**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取的檔案的目錄。<br /><br /> 當定義資料來源目錄指定的目錄，您最常使用的檔案的位置。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果經常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式中的檔案名稱以目錄名稱：`SELECT * FROM C:\MYDIR\EMP`<br /><br /> 或者，您可以指定新的預設目錄使用**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項具有函式。|若要以動態方式設定這個選項，使用**DEFAULTDIR**的呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|

