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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71c80efdb2f4a87537d472ee4b6dc6bdc65af70f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540512"
---
# <a name="appendix-e-scalar-functions"></a>附錄 E：純量函數
ODBC 會指定下列類型的純量函式的每個對應的章節，此附錄中提供這些函式類型的詳細資訊。 函式描述會包含相關聯的語法。  
  
 本附錄包含下列主題。  
  
-   [字串函式](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [數值函式](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [時間、日期和間隔函式](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系統函式](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [明確資料類型轉換函式](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 函式](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC 不會從純量函式要求傳回值的資料類型，因為通常會將資料來源特有的函式。 應用程式應該使用轉換的純量函數時，無法強制執行資料類型轉換。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 和 SQL-92 的純量函式  
 本附錄中的資料表包含已新增在 ODBC 3.0，才能符合 SQL-92 的函式。 定義在 ODBC 中，加入特定類型的純量函數，這些函式會以每個區段。  
  
 ODBC 和 SQL-92 分類其純量函式以不同的方式。 ODBC 純量函式的引數類型，將分類如下：SQL-92 分類它們所傳回的值。 比方說，擷取函式都歸類為 timedate 函式由 ODBC，因為擷取欄位的引數是 datetime 關鍵字，而且擷取來源引數的日期時間或間隔的運算式。 SQL-92，相反地，會將擷取分類為數值純量函數，因為傳回的值是一個數字。  
  
 應用程式可以判斷哪一個驅動程式支援藉由呼叫的純量函式**SQLGetInfo**。 資訊類型為包含適用於 ODBC 和 SQL-92 的純量函數的分類。 這些分類都不同，因為某些純量函式的支援可能會不會對應至 ODBC 和 SQL-92 的資訊類型所示。 例如，支援 ODBC 中的擷取會以 SQL_TIMEDATE_FUNCTIONS 資訊型別;相反地，支援以 SQL-92 的擷取會指示 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 資訊類型。
