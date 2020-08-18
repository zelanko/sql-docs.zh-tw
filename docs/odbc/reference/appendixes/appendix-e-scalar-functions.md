---
description: 附錄 E：純量函式
title: 附錄 E：純量函數 |Microsoft Docs
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
ms.openlocfilehash: 4a814de22df4a97e3c3b3abd0ddc30266fe02a30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411434"
---
# <a name="appendix-e-scalar-functions"></a>附錄 E：純量函式
ODBC 會指定下列類型的純量函數，其中包含在本附錄的對應章節中提供的每個函式類型的詳細資訊。 函數描述包含相關聯的語法。  
  
 本附錄包含下列主題。  
  
-   [字串函式](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [數值函數](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [時間、日期和間隔函式](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系統函式](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [明確資料類型轉換函式](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 函式](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC 不會針對純量函數傳回值的資料類型，因為這些函式通常是資料來源特有的。 應用程式應該盡可能使用 CONVERT 純量函數來強制執行資料類型轉換。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 和 SQL-92 純量函數  
 本附錄中的表格包含已在 ODBC 3.0 中新增的函式，以配合 SQL-92。 針對特定類型的純量函數（如 ODBC 中所定義）所新增的函式會在每個區段中顯示。  
  
 ODBC 和 SQL-92 以不同的方式分類其純量函數。 ODBC 會依引數類型分類純量函數;SQL-92 會依傳回值進行分類。 例如，因為提取欄位引數是 datetime 關鍵字，且解壓縮來源引數是 datetime 或 interval 運算式，所以會將解壓縮函數分類為 ODBC 的 timedate 函式。 另一方面，SQL-92 會將解壓縮分類為數值純量函數，因為傳回值是數值。  
  
 應用程式可以藉由呼叫 **SQLGetInfo**，判斷驅動程式支援哪些純量函數。 ODBC 和適用于純量函數的 SQL-92 分類都包含資訊類型。 因為這些分類不同，所以對某些純量函數的支援可能會在未對應到 ODBC 和 SQL-92 的資訊類型中指出。 例如，在 ODBC 中的 [解壓縮] 支援是由 SQL_TIMEDATE_FUNCTIONS 資訊類型表示。另一方面，SQL-92 中的解壓縮支援是由 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS 資訊類型表示。
