---
title: SQL 最小語法 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20eee34feadb8e3140f25019ec6b0d036ff02e14
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304989"
---
# <a name="sql-minimum-grammar"></a>SQL 最小文法
本節介紹 ODBC 驅動程式必須支援的最低 SQL 語法。 本節中描述的語法是 SQL-92 的入門級語法的子集。  
  
 應用程式可以使用本節中的任何語法,並確保任何符合 ODBC 的驅動程式都將支援該語法。 要確定是否不支援本節中不支援 SQL-92 的其他功能,應用程式應使用SQL_SQL_CONFORMANCE資訊類型調用**SQLGetInfo。** 即使驅動程式不符合任何 SQL-92 符合性級別,應用程式仍可以使用本節中描述的語法。 另一方面,如果驅動程式符合 SQL-92 級別,則驅動程式支援該級別中包含的所有語法。 這包括本節中的語法,因為此處描述的最小語法是最低 SQL-92 符合性級別的純子集。 一旦應用程式知道 SQL-92 級別受支援,它可以通過調用**SQLGetInfo**與與該功能對應的單個資訊類型來確定是否支援更高級別的功能(如果有)。  
  
 僅使用唯讀數據源的驅動程式可能不支援本節中有關更改數據的語法部分。 應用程式可以通過使用SQL_DATA_SOURCE_READ_ONLY資訊類型調用**SQLGetInfo**來確定數據來源是否為唯讀。  
  
## <a name="statement"></a>引數  
 *建立表語句*::*  
  
 建立表*格表名稱*  
  
 (*列識別子資料類型**=,列識別子資料類型**...  
  
> [!IMPORTANT]  
>  作為*創建表語句*中的*資料類型*,應用程式必須使用**SQLGetTypeInfo**返回的結果集TYPE_NAME列中的數據類型。  
  
 *刪除敘述搜尋*::*  
  
 從*表名中移除*[WHERE*搜尋條件*]  
  
 *下拉錶語句*::*  
  
 DROP TABLE*基表名稱*  
  
 *插入敘述*::*  
  
 插入表*名*[(*列識別子*[,*列識別子*))     值 (*插入值**,*插入值*#...  
  
 *select-statement* ::=  
  
 選擇 [所有&#124; *select-list*  
  
 從*表參考清單*  
  
 [WHERE*搜尋條件*]  
  
 [*逐項訂購*]  
  
 *語句*::**建立表語句*  
  
 &#124;*刪除敘述搜尋*  
  
 &#124;*下表語句*  
  
 &#124;*插入敘述*  
  
 &#124;*選擇敘述*  
  
 &#124;*更新敘述搜尋*  
  
 *更新敘述搜尋*  
  
 更新*表格名稱*  
  
 設定*欄位代碼*( &#124;空*表示式*]  
  
 [,*列識別子*] [*運算式*&#124; NULL]...  
  
 [WHERE*搜尋條件*]  
  
 此章節包含下列主題。  
  
-   [SQL 陳述式中使用的項目](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [資料類型支援](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [參數資料類型](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [參數標記](../../../odbc/reference/appendixes/parameter-markers.md)
