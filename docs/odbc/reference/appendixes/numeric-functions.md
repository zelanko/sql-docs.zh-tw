---
title: 數位函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299868"
---
# <a name="numeric-functions"></a>數值函數
下表描述了 ODBC 標量函數集中包含的數位函數。 通過使用SQL_NUMERIC_FUNCTIONS*的資訊類型*調用**SQLGetInfo,** 應用程式可以確定驅動程式支援哪些數值函數。  
  
 除 ABS、ROUND、TRUNCATE、SIGN、FLOOR 和「天花板」之外,所有數值函數都返回數據類型的值SQL_FLOAT,這些值返回與輸入參數相同的數據類型的值。  
  
 表示為*numeric_exp*的參數可以是列的名稱、另一個標量函數的結果或*數位-litera*l,其中基礎數據類型可以表示為SQL_NUMERIC、SQL_DECIMAL、SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER、SQL_BIGINT、SQL_FLOAT、SQL_REAL或SQL_DOUBLE。  
  
 表示為*float_exp*的參數可以是列的名稱、另一個標量函數的結果或*數位文本*,其中基礎數據類型可以表示為SQL_FLOAT。  
  
 表示為*integer_exp*的參數可以是列的名稱、另一個標量函數的結果或*數位文本*,其中基礎數據類型可以表示為SQL_TINYINT、SQL_SMALLINT、SQL_INTEGER或SQL_BIGINT。  
  
 在 ODBC 3.0 中添加了CURRENT_DATE、CURRENT_TIME和CURRENT_TIMESTAMP標量函數,以便與 SQL-92 對齊。  
  
|函式|描述|  
|--------------|-----------------|  
|**ABS (numeric_exp** _numeric_exp_ **)** (ODBC 1.0)|傳*回 numeric_exp*的絕對值 。|  
|**ACOS(** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的弧形作為角度,以弧度表示。|  
|**阿辛 float_exp** _float_exp_ (odBC 1.0) **)**|返回*float_exp*的弧線作為角度,以弧度表示。|  
|**Arot (float_exp** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的弧形作為角度,以弧度表示。|  
|**ATAN2(float_exp1,float_exp2)** _ _(ODBC 2.0) _float_exp2_ **)**|返回*x*和*y*座標的弧形,分別由*float_exp1*和*float_exp2*指定,作為角度,以弧度表示。|  
|**天花板 (numeric_exp** _numeric_exp_ **)** (ODBC 1.0)|返回大於或等於*numeric_exp*的最小整數。 返回值與輸入參數的數據類型相同。|  
|**COS(** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的可成因,其中*float_exp*是以弧度表示的角度。|  
|**COT(** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的共量,其中*float_exp*是以弧度表示的角度。|  
|**學位(numeric_exp** _numeric_exp_ **)** (ODBC 2.0)|返回從*numeric_exp*弧度轉換的度數。|  
|**EXP(** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的指數值。|  
|**地板(numeric_exp** _numeric_exp_ **)** (ODBC 1.0)|返回小於或等於*numeric_exp*的最大整數。 返回值與輸入參數的數據類型相同。|  
|**紀錄(float_exp** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的自然對數。|  
|**紀錄10(float_exp** _float_exp_ **)** (ODBC 2.0)|返回*float_exp*的基 10 對數。|  
|**MOD(integer_exp1,integer_exp2** _integer_exp1_ _ _ **)** (ODBC 1.0)|傳*回 integer_exp1*的剩餘數(模數)除以*integer_exp2*。|  
|**PI(** (ODBC 1.0)|將 pi 的常量值作為浮點值返回。|  
|**電源(numeric_exp** _numeric_exp_ _,integer_exp_**)** (ODBC 2.0)|將*numeric_exp*的值返回到*integer_exp*的功率。|  
|**拉迪安斯**_(numeric_exp_ **)** (ODBC 2.0)|返回從*numeric_exp*度轉換的弧度數。|  
|**蘭德 (**[*integer_exp*+**)** (ODBC 1.0)|使用*integer_exp*作為可選種子值返回隨機浮點值。|  
|**圓 (numeric_exp** _ _, _integer_exp_**)** (ODBC 2.0)|*返回numeric_exp*捨入到小數點右側*integer_exp*位。 如果*integer_exp*為負數,*則numeric_exp*將四捨五入到 *&#124;integer_exp*小數點左側的&#124;位。|  
|**標誌(numeric_exp** _numeric_exp_ **)(ODBC** 1.0)|返回*numeric_exp*標誌的指示器。 如果*numeric_exp*小於零,則返回 -1。 如果*numeric_exp*等於零,則返回 0。 如果*numeric_exp*大於零,則返回1。|  
|**SIN(** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的正則,其中*float_exp*是以弧度表示的角度。|  
|**SQRT(** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的平方根。|  
|**褐色(float_exp** _float_exp_ **)** (ODBC 1.0)|返回*float_exp*的切線,其中*float_exp*是以弧度表示的角度。|  
|**(numeric_exp,** _ _ _ _integer_exp **)** (ODBC 2.0)|*返回numeric_exp*截斷到小數點右側*integer_exp*位。 如果*integer_exp*為負數,*則numeric_exp*將被截斷為&#124;*integer_exp*小數點左側的&#124;位。|
