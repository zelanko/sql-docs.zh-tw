---
title: "附錄 e： 純量函數 |Microsoft 文件"
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
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aaa110a6a62ca91535e790a267ef714675719bf4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="appendix-e-scalar-functions"></a>附錄 e： 純量函數
ODBC 會指定下列類型的純量函數，與每個對應的章節，此附錄中提供這些函式類型的詳細資訊。 函式描述包含相關聯的語法。  
  
 本附錄包含下列主題。  
  
-   [字串函式](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [數值函數](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [時間、 日期和間隔函數](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系統函式](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [明確資料類型轉換函式](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL 92 CAST 函數](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC 不會要求傳回值的資料類型從純量函式因為函式通常是資料來源專用。 應用程式應該使用轉換的純量函數時，無法強制執行資料類型轉換。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 和 SQL 92 純量函數  
 本附錄中的資料表包含已加入以配合 SQL 92 ODBC 3.0 中的函式。 定義在 ODBC 中，加入針對特定類型的純量函數，這些函式會以每個區段。  
  
 ODBC 和 SQL 92 以不同方式分類其純量函數。 ODBC 純量函數的引數類型，將分類如下：SQL 92 分類它們所傳回的值。 例如，EXTRACT 函式都歸類為 timedate 函式由 ODBC，因為擷取欄位引數是 datetime 關鍵字，而且擷取來源引數的日期時間或間隔的運算式。 Sql-92，相反地，會將擷取分類為數值的純量函數，因為傳回值是數字。  
  
 應用程式就可以判斷哪一個驅動程式支援藉由呼叫的純量函數**SQLGetInfo**。 還是包含適用於 ODBC 和 SQL 92 分類純量函數的資訊類型。 這些分類則不同，因為某些純量函數的支援可能會以未對應到 ODBC 和 sql-92 的資訊類型。 擷取 ODBC 中的支援，例如以 SQL_TIMEDATE_FUNCTIONS 資訊類型。相反地，支援以 sql-92，擷取會指示 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 資訊類型。
