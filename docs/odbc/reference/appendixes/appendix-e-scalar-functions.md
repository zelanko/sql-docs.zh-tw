---
title: 附錄 E：純量函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea354a7f882bd1a75c5f16fb19350d69ca11d375
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292488"
---
# <a name="appendix-e-scalar-functions"></a>附錄 E：純量函式
ODBC 會指定下列類型的純量函數，其中包含本附錄的對應章節中所提供的每個函數類型的詳細資訊。 函數描述包含相關聯的語法。  
  
 本附錄包含下列主題。  
  
-   [字串函式](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [數值函數](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [時間、日期和間隔函式](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系統函數](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [明確資料類型轉換函式](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 函式](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC 不會針對純量函數強制傳回值的資料類型，因為函式通常是資料來源特有的。 應用程式應該盡可能使用 CONVERT 純量函數來強制轉換資料類型。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 和 SQL-92 純量函數  
 本附錄中的表格包含已在 ODBC 3.0 中加入以配合 SQL-92 的函式。 針對特定類型的純量函數（如 ODBC 中所定義）所新增的函式，會在每個區段中指出。  
  
 ODBC 和 SQL-92 會以不同的方式分類其純量函數。 ODBC 會依引數類型來分類純量函數;SQL-92 根據傳回值來分類它們。 例如，因為「解壓縮欄位」引數是 datetime 關鍵字，而「解壓縮-來源」引數是 datetime 或 interval 運算式，所以此解壓縮函數會由 ODBC 分類為 timedate 時間函數。 另一方面，SQL-92 會將解壓縮分類為數值純量函數，因為傳回值是數值。  
  
 應用程式可以藉由呼叫**SQLGetInfo**來判斷驅動程式支援哪些純量函數。 包括 ODBC 和純量函式之 SQL-92 分類的資訊類型。 由於這些分類不同，因此可能會在未對應至 ODBC 和 SQL-92 的資訊類型中指出對某些純量函數的支援。 例如，ODBC 中的 [解壓縮] 支援是以 SQL_TIMEDATE_FUNCTIONS 資訊類型表示;另一方面，在 SQL-92 中的解壓縮支援是以 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 資訊類型來表示。
