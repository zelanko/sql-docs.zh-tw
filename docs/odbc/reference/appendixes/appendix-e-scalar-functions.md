---
title: '附錄 E: Scalar 功能 |微軟文件'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292488"
---
# <a name="appendix-e-scalar-functions"></a>附錄 E：純量函式
ODBC 指定以下類型的標量函數,並詳細介紹了本附錄相應部分中提供的每種函數類型。 函數描述包括關聯的語法。  
  
 本附錄包含以下主題。  
  
-   [字串函式](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [數位函數](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [時間、日期和間隔函式](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [系統功能](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [明確資料類型轉換函式](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [SQL-92 CAST 函式](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC 不強制使用類型來獲取標量函數的返回值,因為這些函數通常是特定於數據源的。 應用程式應盡可能使用 CONVERT 標量函數來強制轉換數據類型。  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC 與 SQL-92 Scalar 函式  
 本附錄中的表包括已在 ODBC 3.0 中添加的函數,以便與 SQL-92 對齊。 為特定類型的標量函數添加的函數(如 ODBC 中定義)在每個部分都表示。  
  
 ODBC 和 SQL-92 對其標量函數分類不同。 ODBC 按參數類型對標量函數進行分類;SQL-92 按返回值對其進行分類。 例如,EXTRACT 函數被 ODBC 分類為時間日期函數,因為提取欄位參數是日期時間關鍵字,並且提取源參數是日期時間或間隔表達式。 另一方面,SQL-92 將 EXTRACT 分類為數字標量函數,因為返回值是一個數位。  
  
 應用程式可以通過調用**SQLGetInfo**來確定驅動程式支援哪些標量函數。 對於 ODBC 和標量函數的 SQL-92 分類,都包含資訊類型。 由於這些分類不同,因此某些標量函數的支援可能以與 ODBC 和 SQL-92 不對應的資訊類型指示。 例如,ODBC 中對 EXTRACT 的支援由SQL_TIMEDATE_FUNCTIONS資訊類型指示;另一方面,SQL-92 中對 EXTRACT 的支援由SQL_SQL92_NUMERIC_VALUE_FUNCTIONS資訊類型指示。
