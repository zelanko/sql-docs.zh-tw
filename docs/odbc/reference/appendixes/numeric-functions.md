---
title: 數值函數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 03da5b6644e0f7df3dc4e5e16a211cb503023bad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299868"
---
# <a name="numeric-functions"></a>數值函數
下表描述包含在 ODBC 純量函數集內的數值函數。 藉由使用 SQL_NUMERIC_FUNCTIONS 的*資訊類型*呼叫**SQLGetInfo** ，應用程式可以判斷驅動程式支援哪些數值函數。  
  
 除了 ABS、ROUND、截斷、正負號、樓層和上限（傳回與輸入參數相同資料類型的值）以外，所有數值函數都會傳回資料類型 SQL_FLOAT 的值。  
  
 表示為*numeric_exp*的引數可以是資料行的名稱、另一個純量函數的結果，或*數值 litera*l，其中基礎資料類型可能會表示為 SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL 或 SQL_DOUBLE。  
  
 表示為*float_exp*的引數可以是資料行的名稱、另一個純量函數的結果，或*數值常*值，其中基礎資料類型可以表示為 SQL_FLOAT。  
  
 表示為*integer_exp*的引數可以是資料行的名稱、另一個純量函數的結果，或*數值常*值，其中基礎資料類型可以表示為 SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER 或 SQL_BIGINT。  
  
 ODBC 3.0 中已加入 CURRENT_DATE、CURRENT_TIME 和 CURRENT_TIMESTAMP 純量函數，以配合 SQL-92。  
  
|函式|描述|  
|--------------|-----------------|  
|**ABS （** _numeric_exp_ **）** （ODBC 1.0）|傳回*numeric_exp*的絕對值。|  
|**ACOS （** _float_exp_ **）** （ODBC 1.0）|以弧度表示的角度傳回*float_exp*的反余弦。|  
|**ASIN （** _float_exp_ **）** （ODBC 1.0）|以弧度表示的角度傳回*float_exp*的反正弦。|  
|**ATAN （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的反正切值（以弧度表示）。|  
|**ATAN2 （** _float_exp1_， _float_exp2_**）** （ODBC 2.0）|傳回*x*和*y*座標的反正切值，分別由*float_exp1*和*float_exp2*指定為角度，以弧度表示。|  
|**上限（** _numeric_exp_ **）** （ODBC 1.0）|傳回大於或等於*numeric_exp*的最小整數。 傳回值與輸入參數的資料類型相同。|  
|**COS （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的余弦值，其中*float_exp*是以弧度表示的角度。|  
|**COT （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的餘切，其中*float_exp*是以弧度表示的角度。|  
|**度數（** _numeric_exp_ **）** （ODBC 2.0）|傳回從*numeric_exp*弧度轉換的度數數目。|  
|**EXP （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的指數值。|  
|**FLOOR （** _numeric_exp_ **）** （ODBC 1.0）|傳回小於或等於*numeric_exp*的最大整數。 傳回值與輸入參數的資料類型相同。|  
|**LOG （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的自然對數。|  
|**LOG10 （** _float_exp_ **）** （ODBC 2.0）|傳回*float_exp*的以10為底數的對數。|  
|**MOD （** _integer_exp1_， _integer_exp2_**）** （ODBC 1.0）|傳回*integer_exp1*除以*integer_exp2*的餘數（模數）。|  
|**PI （）** （ODBC 1.0）|傳回 pi 的常數值做為浮點值。|  
|**POWER （** _numeric_exp_， _integer_exp_**）** （ODBC 2.0）|將*numeric_exp*的值傳回*integer_exp*的乘冪。|  
|**弧度（** _numeric_exp_ **）** （ODBC 2.0）|傳回從*numeric_exp*度轉換的弧度數。|  
|**RAND （**[*integer_exp*]**）** （ODBC 1.0）|使用*integer_exp*做為選擇性的種子值，傳回隨機的浮點值。|  
|**ROUND （** _numeric_exp_， _integer_exp_**）** （ODBC 2.0）|傳回*numeric_exp*四捨五入至小數點右方*integer_exp*位置。 如果*integer_exp*為負數， *numeric_exp*會四捨五入為 &#124;*integer_exp*&#124; 位在小數點左邊。|  
|**SIGN （** _numeric_exp_ **）** （ODBC 1.0）|傳回*numeric_exp*正負號的指標。 如果*numeric_exp*小於零，則會傳回-1。 如果*numeric_exp*等於零，則會傳回0。 如果*numeric_exp*大於零，則會傳回1。|  
|**SIN （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的正弦值，其中*float_exp*是以弧度表示的角度。|  
|**SQRT （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的平方根。|  
|**TAN （** _float_exp_ **）** （ODBC 1.0）|傳回*float_exp*的正切函數，其中*float_exp*是以弧度表示的角度。|  
|**截斷（** _numeric_exp_、 _integer_exp_**）** （ODBC 2.0）|傳回*numeric_exp*截斷為小數點右邊的*integer_exp*位置。 如果*integer_exp*為負數， *numeric_exp*會被截斷為 &#124;*integer_exp*&#124; 小數點左邊的位置。|
