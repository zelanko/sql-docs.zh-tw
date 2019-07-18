---
title: 設定文字檔驅動程式以程式設計方式的選項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1a28e5c7ccf3c701e5f97440cd97ed843ab53dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063499"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>以程式設計方式設定文字檔驅動程式的選項

|選項|描述|方法|  
|------------|-----------------|------------|  
|資料來源名稱|識別資料來源，例如薪資或人員的名稱。|若要以動態方式設定此選項，請使用**DSN**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|定義格式|顯示**定義文字格式** 對話方塊中，並可讓您指定資料來源目錄中的個別資料表的結構描述。|無法以動態方式設定這個選項，藉由呼叫[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|描述|資料來源中資料的選擇性描述比方說，「 雇用日期、 薪資記錄以及目前檢閱所有員工。 」|若要以動態方式設定此選項，請使用**描述**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|目錄|選取的目標的目錄。|若要以動態方式設定此選項，請使用**DEFAULTDIR**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|延伸模組清單|列出資料來源上的文字檔案的副檔名。 使用文字驅動程式時，使用具有不含副檔名的名稱執行 CREATE TABLE 陳述式時，會建立不含副檔名的檔案。 提供不含副檔名時，其他驅動程式會建立檔案與預設延伸模組。 若要建立副檔名為.txt 的檔案，必須在名稱中包含擴充功能。 若要顯示檔案中的延伸模組不**定義文字格式** 對話方塊中，"*。 」 必須新增至延伸模組清單。|若要以動態方式設定此選項，請使用**延伸模組**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|唯讀|指定資料庫為唯讀。|若要以動態方式設定此選項，請使用**READONLY**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|要掃描的資料列|掃描以判斷每個資料行的資料類型的資料列數目。 指定找到的資料類型的最大數目來決定的資料類型。 如果發生資料不符合猜對的資料行的資料類型，將傳回的資料類型，為 NULL 值。<br /><br /> 文字驅動程式，您可能輸入的數字 1 到 32767 之間的掃描; 的資料列數目不過，此值永遠都會預設為 25。 （限制以外的數字會傳回錯誤）。|若要以動態方式設定此選項，請使用**於 MAXSCANROWS**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|  
|選取目錄|顯示的對話方塊，您可以在其中選取包含您想要存取的檔案的目錄。<br /><br /> 當定義資料來源目錄指定的目錄，您最常使用的檔案的位置。 ODBC 驅動程式會使用此目錄，做為預設目錄。 如果較常使用，請將其他檔案複製到這個目錄中。 或者，您可以限定在 SELECT 陳述式與目錄名稱的檔案名稱： `SELECT * FROM C:\MYDIR\EMP`<br /><br /> 或者，您可以藉由指定新的預設目錄**SQLSetConnectOption** SQL_CURRENT_QUALIFIER 選項的函式。|若要以動態方式設定此選項，請使用**DEFAULTDIR**呼叫中的關鍵字[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。|
