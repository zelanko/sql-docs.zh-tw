---
title: 數值函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca33d451fe5e1431d9bc4fb29196b98adcfb933f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620366"
---
# <a name="numeric-functions"></a>數值函數
下表描述 ODBC 純量函式集合中包含的數值函式。 藉由呼叫**SQLGetInfo**具有*資訊類型*的 SQL_NUMERIC_FUNCTIONS，應用程式可以判斷驅動程式支援的數值函式。  
  
 所有的數值函式會傳回值的資料型別除了 ABS，SQL_FLOAT ROUND、 TRUNCATE、 符號、 樓層、 和上限，會傳回相同的資料值的類型做為輸入參數。  
  
 引數可以分成*則 numeric_exp*可以是資料行的名稱，另一個的純量函式的結果或*數值 litera*l，其中可能表示基礎資料類型為 SQL_NUMERIC，SQL_DECIMAL SQL_TINYINT、 SQL_SMALLINT、 SQL_INTEGER、 SQL_BIGINT、 SQL_FLOAT、 SQL_REAL，還是 SQL_DOUBLE。  
  
 引數可以分成*float_exp*可以是資料行的名稱，另一個的純量函式的結果或*數值常值*，其中可以當做 SQL_FLOAT 表示基礎資料類型。  
  
 引數可以分成*integer_exp*可以是資料行的名稱，另一個的純量函式的結果或*數值常值*，其中表示基礎資料類型，為 SQL_TINYINT，SQL_SMALLINT、 SQL_INTEGER 或 SQL_BIGINT。  
  
 在 ODBC 3.0，才能符合 SQL-92 收錄 CURRENT_DATE、 CURRENT_TIME 和 CURRENT_TIMESTAMP 純量函式。  
  
|函數|描述|  
|--------------|-----------------|  
|**ABS (** *則 numeric_exp* **)** (ODBC 1.0)|傳回數值的絕對值*則 numeric_exp*。|  
|**ACOS (** *float_exp* **)** (ODBC 1.0)|傳回的反餘弦*float_exp*以角度，以弧度表示。|  
|**ASIN (** *float_exp* **)** (ODBC 1.0)|傳回的反正弦*float_exp*以角度，以弧度表示。|  
|**ATAN (** *float_exp* **)** (ODBC 1.0)|傳回的反正切*float_exp*以角度，以弧度表示。|  
|**ATAN2 (** *float_exp1*， *float_exp2 * * *)** (ODBC 2.0)|傳回的反正切*x*並*y*所指定的座標*float_exp1*並*float_exp2*分別角度，以弧度為單位來表示。|  
|**CEILING (** *則 numeric_exp* **)** (ODBC 1.0)|傳回的最小整數，大於或等於*則 numeric_exp*。 傳回的值屬於相同的資料類型當做輸入參數。|  
|**COS (** *float_exp* **)** (ODBC 1.0)|傳回的餘弦*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**COT (** *float_exp* **)** (ODBC 1.0)|餘切函數會傳回*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**度 (** *則 numeric_exp* **)** (ODBC 2.0)|傳回從轉換的度數*則 numeric_exp*弧度為單位。|  
|**EXP (** *float_exp* **)** (ODBC 1.0)|傳回指數值*float_exp*。|  
|**FLOOR (** *則 numeric_exp* **)** (ODBC 1.0)|傳回小於或等於最大整數*則 numeric_exp*。 傳回的值屬於相同的資料類型當做輸入參數。|  
|**記錄檔 (** *float_exp* **)** (ODBC 1.0)|傳回自然對數*float_exp*。|  
|**LOG10 (** *float_exp* **)** (ODBC 2.0)|傳回基底 10 對數*float_exp*。|  
|**MOD (** *integer_exp1*， *integer_exp2 * * *)** (ODBC 1.0)|傳回的餘數 （模數） *integer_exp1*除以*integer_exp2*。|  
|**PI （)** (ODBC 1.0)|傳回 pi 的常數值為浮點值。|  
|**POWER (** *則 numeric_exp*， *integer_exp * * *)** (ODBC 2.0)|傳回的值*則 numeric_exp*冪*integer_exp*。|  
|**弧度為單位 (** *則 numeric_exp* **)** (ODBC 2.0)|傳回從轉換的弧度的數目*則 numeric_exp*度。|  
|**RAND (**[*integer_exp*]**)** (ODBC 1.0)|傳回隨機浮點數的值，使用*integer_exp*做為選擇性的種子值。|  
|**ROUND (** *則 numeric_exp*， *integer_exp * * *)** (ODBC 2.0)|傳回*則 numeric_exp*捨入到*integer_exp*會放在小數點右邊。 如果*integer_exp*是負數*則 numeric_exp 就*會捨入到&#124; *integer_exp* &#124;會放在小數點左邊。|  
|**符號 (** *則 numeric_exp* **)** (ODBC 1.0)|傳回的正負號的指標*則 numeric_exp*。 如果*則 numeric_exp*為小於零，-1 會傳回。 如果*則 numeric_exp*等於零，就會傳回 0。 如果*則 numeric_exp*是小於或等於零，則傳回 1。|  
|**SIN (** *float_exp* **)** (ODBC 1.0)|傳回正弦*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**SQRT (** *float_exp* **)** (ODBC 1.0)|傳回平方根*float_exp*。|  
|**TAN (** *float_exp* **)** (ODBC 1.0)|傳回正切*float_exp*，其中*float_exp*是角度以弧度表示。|  
|**截斷 (** *則 numeric_exp*， *integer_exp * * *)** (ODBC 2.0)|傳回*則 numeric_exp*截斷成*integer_exp*會放在小數點右邊。 如果*integer_exp*是負數*則 numeric_exp*會被截斷成&#124; *integer_exp* &#124;會放在小數點左邊。|
