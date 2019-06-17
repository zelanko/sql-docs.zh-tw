---
title: SQL 最小文法 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26cf76200010edae7f85993ec33eb3722f35e94e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270503"
---
# <a name="sql-minimum-grammar"></a>SQL 最小文法
本節描述 ODBC 驅動程式必須支援的最小 SQL 語法。 在本節中所述的語法是以 SQL-92 的項目層級語法子集。  
  
 應用程式可以使用任何語法的這一節，並確保任何符合 ODBC 規範的驅動程式會支援該語法。 若要判斷是否支援 SQL-92 不在這一節中的其他功能，應用程式應該呼叫**SQLGetInfo** SQL_SQL_CONFORMANCE 資訊類型。 即使驅動程式不符合任何 SQL-92 一致性層級，則應用程式仍然可以使用這一節所述的語法。 如果驅動程式符合 SQL-92 層級，相反地，它支援在該層級中包含的所有語法。 因為這裡所述的最小文法是純粹的子集的最低 SQL-92 一致性層級，這可以包括在這一節中的語法。 一旦應用程式知道支援的 SQL-92 層級，它可以判斷是否較高層級的功能支援 （是否有的話） 藉由呼叫**SQLGetInfo**對應至該功能的個別資訊類型。  
  
 僅適用於唯讀資料來源的驅動程式可能不支援這一節包含文法的處理變更資料的這些組件。 應用程式可以判斷資料來源是否唯讀藉由呼叫**SQLGetInfo** SQL_DATA_SOURCE_READ_ONLY 資訊類型。  
  
## <a name="statement"></a>引數  
 *create-table-statement* ::=  
  
 CREATE TABLE*基底資料表名稱*  
  
 (*資料行識別碼資料型別*[ *，資料行識別碼資料型別*]...)  
  
> [!IMPORTANT]  
>  作為*資料型別*中*建立資料表陳述式*，應用程式必須使用來自 TYPE_NAME 資料行所傳回的結果集的資料型別**SQLGetTypeInfo**。  
  
 *delete-statement-searched* ::=  
  
 DELETE FROM *table-name* [WHERE *search-condition*]  
  
 *drop-table-statement* ::=  
  
 DROP TABLE*基底資料表名稱*  
  
 *insert-statement* ::=  
  
 INSERT INTO *table-name* [( *column-identifier* [, *column-identifier*]...)]      VALUES (*insert-value*[, *insert-value*]... )  
  
 *select-statement* ::=  
  
 SELECT [ALL &#124; DISTINCT] *select-list*  
  
 從*資料表參考清單*  
  
 [WHERE *search-condition*]  
  
 [*order-by-clause*]  
  
 *statement* ::= *create-table-statement*  
  
 &#124; *delete-statement-searched*  
  
 &#124; *drop-table-statement*  
  
 &#124; *insert-statement*  
  
 &#124; *select-statement*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-searched*  
  
 更新*資料表名稱*  
  
 SET *column-identifier* = {*expression* &#124; NULL }  
  
 [，*資料行識別碼*= {*運算式* &#124; NULL}]...  
  
 [WHERE *search-condition*]  
  
 此章節包含下列主題。  
  
-   [SQL 陳述式中使用的項目](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [資料類型支援](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [參數資料類型](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [參數標記](../../../odbc/reference/appendixes/parameter-markers.md)
