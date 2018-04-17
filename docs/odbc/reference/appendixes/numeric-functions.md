---
title: 數值函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- functions [ODBC], numeric functions
- numeric functions [ODBC]
ms.assetid: 4fa548dc-e8b0-4179-92ff-81d6a79d10c3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd6bcf73b63e6fdf5dc61209ed990955c19e7851
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="numeric-functions"></a>數值函數
下表描述 ODBC 純量函式集合中包含的數值函式。 藉由呼叫**SQLGetInfo**與*資訊類型*的 SQL_NUMERIC_FUNCTIONS，應用程式可以判斷驅動程式支援哪些數值的函式。  
  
 所有的數值函式會傳回值的資料型別除了 ABS，SQL_FLOAT ROUND、 TRUNCATE、 符號、 FLOOR、 和上限，會傳回相同的資料值類型做為輸入參數。  
  
 引數表示為*則 numeric_exp 就*可以是資料行的名稱，另一個純量函數的結果或*數值 litera*l，其中基礎資料類型可以表示為 SQL_NUMERIC，SQL_DECIMAL、 SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT SQL_REAL 或 SQL_DOUBLE。  
  
 引數表示為*float_exp*可以是資料行的名稱，另一個純量函數的結果或*數值常值*，其中表示基礎資料類型，當做 SQL_FLOAT。  
  
 引數表示為*integer_exp*可以是資料行的名稱，另一個純量函數的結果或*數值常值*，其中基礎資料類型可以表示成 SQL_TINYINT，SQL_SMALLINT、 SQL_INTEGER 或 SQL_BIGINT。  
  
 在 ODBC 3.0 以配合 SQL 92 已加入 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP 純量函數。  
  
|函數|Description|  
|--------------|-----------------|  
|**ABS (** *則 numeric_exp 就* **)** (ODBC 1.0)|傳回數值的絕對值*則 numeric_exp 就*。|  
|**ACOS (** *float_exp* **)** (ODBC 1.0)|傳回的反餘弦*float_exp*為一角度，以弧度表示。|  
|**ASIN (** *float_exp* **)** (ODBC 1.0)|傳回的反正弦值*float_exp*為一角度，以弧度表示。|  
|**ATAN (** *float_exp* **)** (ODBC 1.0)|傳回的反正切值*float_exp*為一角度，以弧度表示。|  
|**ATAN2 (** *float_exp1*， *float_exp2 * * *)** (ODBC 2.0)|傳回的反正切值*x*和*y*所指定的座標*float_exp1*和*float_exp2*，分別代表角度以弧度為單位表示。|  
|**CEILING (** *則 numeric_exp 就* **)** (ODBC 1.0)|大於或等於傳回的最小整數*則 numeric_exp 就*。 傳回值是相同的資料類型，做為輸入參數。|  
|**COS (** *float_exp* **)** (ODBC 1.0)|傳回的餘弦*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**COT (** *float_exp* **)** (ODBC 1.0)|傳回的餘切值*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**度 (** *則 numeric_exp 就* **)** (ODBC 2.0)|傳回從轉換的度數*則 numeric_exp 就*弧度為單位。|  
|**EXP (** *float_exp* **)** (ODBC 1.0)|傳回指數值*float_exp*。|  
|**FLOOR (** *則 numeric_exp 就* **)** (ODBC 1.0)|傳回小於或等於最大整數*則 numeric_exp 就*。 傳回值是相同的資料類型，做為輸入參數。|  
|**記錄檔 (** *float_exp* **)** (ODBC 1.0)|傳回自然對數*float_exp*。|  
|**LOG10 (** *float_exp* **)** (ODBC 2.0)|傳回基底 10 對數*float_exp*。|  
|**MOD (** *integer_exp1*， *integer_exp2 * * *)** (ODBC 1.0)|傳回的其餘部分 （模數） *integer_exp1*除以*integer_exp2*。|  
|**PI （)** (ODBC 1.0)|傳回 pi 的常數值為浮點值。|  
|**POWER (** *則 numeric_exp 就*， *integer_exp * * *)** (ODBC 2.0)|傳回的值*則 numeric_exp 就*冪*integer_exp*。|  
|**弧度為單位 (** *則 numeric_exp 就* **)** (ODBC 2.0)|傳回弧度從轉換的數字*則 numeric_exp 就*度。|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|傳回隨機浮點值。 使用*integer_exp*做為選擇性的種子值。|  
|**ROUND (** *則 numeric_exp 就*， *integer_exp * * *)** (ODBC 2.0)|傳回*則 numeric_exp 就*捨入到*integer_exp*會放在小數點右邊。 如果*integer_exp*是負數，*則 numeric_exp 就*會捨入到&#124; *integer_exp* &#124;放置小數點左邊。|  
|**符號 (** *則 numeric_exp 就* **)** (ODBC 1.0)|傳回的正負號的指標*則 numeric_exp 就*。 如果*則 numeric_exp 就*為小於零，-1 會傳回。 如果*則 numeric_exp 就*等於零，則傳回 0。 如果*則 numeric_exp 就*大於零，則傳回 1。|  
|**SIN (** *float_exp* **)** (ODBC 1.0)|傳回正弦*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**SQRT (** *float_exp* **)** (ODBC 1.0)|傳回平方根*float_exp*。|  
|**TAN (** *float_exp* **)** (ODBC 1.0)|傳回正切*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**TRUNCATE (** *則 numeric_exp 就*， *integer_exp * * *)** (ODBC 2.0)|傳回*則 numeric_exp 就*截斷成*integer_exp*會放在小數點右邊。 如果*integer_exp*是負數，*則 numeric_exp 就*會被截斷成&#124; *integer_exp* &#124;放置小數點左邊。|
