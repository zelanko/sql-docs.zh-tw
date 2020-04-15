---
title: SQL 類型識別子 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95bf46844e9ed91aac1ec6cb93a298995f0901d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299768"
---
# <a name="sql-type-identifiers"></a>SQL 類型識別碼
每個數據源定義其自己的 SQL 數據類型。 ODBC 定義類型識別碼,並描述可能映射到每個類型識別碼的 SQL 資料類型的一般特徵。 它是特定於驅動程式的基礎資料來源中每個數據類型映射到 ODBC 的 SQL 類型識別碼的。  
  
 例如,SQL_CHAR是具有固定長度(通常介於 1 到 254 個字元)的字元列的類型標識符。 這些特徵對應於許多 SQL 資料來源中的 CHAR 資料類型。 因此,當應用程式發現列的類型標識符SQL_CHAR時,它可以假定它可能正在處理 CHAR 列。 但是,在假定列介於 1 到 254 個字元之間之前,它仍應檢查列的位元組長度;例如,非 SQL 資料來源的驅動程式可能會將 500 個字元的固定長度字元列映射到SQL_CHAR或SQL_LONGVARCHAR,因為兩者都不是完全匹配的。  
  
 ODBC 定義了多種 SQL 類型識別碼。 但是,驅動程式不需要使用所有這些標識符。 相反,它只使用它需要的標識符來公開基礎數據來源支援的 SQL 資料類型。 如果基礎資料來源支援沒有類型識別碼對應的 SQL 資料類型,則驅動程式可以定義其他類型識別碼。 有關詳細資訊,請參閱[特定於驅動程式的資料類型、描述符類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
 有關 SQL 類型識別碼的完整說明,請參閱附錄 D 中的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md):資料類型。
