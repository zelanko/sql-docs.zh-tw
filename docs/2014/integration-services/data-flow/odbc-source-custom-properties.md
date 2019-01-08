---
title: ODBC 來源自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 362bbcd8-b7b0-4bab-8afe-1212b2ad1af9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fd7d2564d35f28130289ff08d3824a6ed4a75d21
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754650"
---
# <a name="odbc-source-custom-properties"></a>ODBC Source Custom Properties
  下表將描述 ODBC 來源的自訂屬性。 所有屬性都可從 SSIS 屬性運算式設定。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|連接|ODBC 連接|用來存取來源資料庫的 ODBC 連接。|  
|AccessMode|整數 (列舉)|用來存取資料庫的模式。 可能值為資料表名稱 (0) 和 SQL 命令(1)。<br /><br /> 預設值為資料表名稱 (0)。|  
|BatchSize|Integer|大量擷取的批次大小。 這是當做陣列擷取的記錄數目。 如果選定的 ODBC 提供者不支援陣列，批次大小為 1。|  
|BindCharColumnAs|整數 (列舉)|此屬性決定 ODBC 來源如何繫結具有多位元組字串類型 (如 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR) 的資料行。<br /><br /> 可能值為 Unicode (0) 和 ANSI (1)。前者繫結 SQL_C_WCHAR 等資料行，後者則繫結 SQL_C_CHAR 等資料行。 預設值為 Unicode (0)。<br /><br /> **注意**:這個屬性不適用於**ODBC 來源編輯器**，但可以透過設定**進階編輯器**。|  
|BindNumericAs|整數 (列舉)|此屬性決定 ODBC 來源如何繫結具有 SQL_TYPE_NUMERIC 和 SQL_TYPE_DECIMAL 資料類型之數值資料的資料行。<br /><br /> 可能的選項為 Char (0) 和 Numeric (1)。前者繫結 SQL_C_CHAR 等資料行，後者則繫結 SQL_C_NUMERIC 等資料行。 預設值為 Char (0)。<br /><br /> **注意**:這個屬性不適用於**ODBC 來源編輯器**，但可以透過設定**進階編輯器**。|  
|DefaultCodePage|Integer|要用於字串輸出資料行的字碼頁。<br /><br /> **注意**:這個屬性不適用於**ODBC 來源編輯器**，但可以透過設定**進階編輯器**。|  
|ExposeCharColumnsAsUnicode|布林|此屬性決定元件如何公開 CHAR 資料行。 預設值為 False，表示 CHAR 資料行公開為多位元組字串 (DT_STR)。 如果為 True，則 CHAR 資料行公開為寬字元字串 (DT_WSTR)。<br /><br /> **注意**:這個屬性不適用於**ODBC 來源編輯器**，但可以透過設定**進階編輯器**。|  
|FetchMethod|整數 (列舉)|用於取得資料的方法。 可能的選項為逐列 (0) 和批次 (1)。 預設值為批次 (1)。<br /><br /> 如需這些選項的詳細資訊，請參閱 [ODBC Source](odbc-source.md)。<br /><br /> **注意**:這個屬性不適用於**ODBC 來源編輯器**，但可以透過設定**進階編輯器**。|  
|SqlCommand|String|當 AccessMode 設為 [SQL 命令] 時要執行的 SQL 命令。|  
|StatementTimeout|Integer|在傳回至應用程式並出現錯誤之前等候 SQL 陳述式執行的秒數。 預設值為 0。 值為 0 表示系統不會逾時。|  
|TableName|String|當 AccessMode 設為 [資料表名稱] 時所使用之資料的資料表名稱。|  
|LobChunckSize|Integer|LOB 資料行的區塊大小配置。|  
||||  
  
## <a name="see-also"></a>另請參閱  
 [ODBC Source](odbc-source.md)   
 [ODBC 來源編輯器 &#40;連線管理員頁面&#41;](../odbc-source-editor-connection-manager-page.md)  
  
  
