---
title: 顯示大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61afd5c9932f58c49e54b4aff8b053d0a25a6e3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130016"
---
# <a name="display-size"></a>顯示大小
資料行的顯示大小是以字元形式顯示資料所需的最大字元數。 下表定義每個 ODBC SQL 資料類型的顯示大小。  
  
|SQL 類型識別碼|顯示大小|  
|-------------------------|------------------|  
|所有字元類型 [a]|針對以字元形式顯示資料所需的字元數（針對固定類型）或最大值（針對變數類型）。|  
|SQL_DECIMAL SQL_NUMERIC|資料行的精確度加上2（正負號、*有效位數和*小數點）。 例如，定義為 NUMERIC （10，3）之資料行的顯示大小為12。|  
|SQL_BIT|1（1個數字）。|  
|SQL_TINYINT|如果帶正負號，則為4（符號和3位數）或3（如果未簽署（3位數））。|  
|SQL_SMALLINT|如果帶正負號，則為6（符號和5位數）或5（如果未簽署（5位數））。|  
|SQL_INTEGER|如果帶正負號，則為11（符號和10位數）或10（如果未簽署（10位數））。|  
|SQL_BIGINT|20（如果帶正負號，則為符號和19位數，如果未簽署，則為20位數）。|  
|SQL_REAL|14（正負號、7位數、小數點、字母*E*、正負號及2位數）。|  
|SQL_FLOAT SQL_DOUBLE|24（正負號、15位數、小數點、字母*E*、正負號及3位數）。|  
|所有二進位類型 [a]|資料行的已定義或最大值（針對變數類型）的長度為2。 （每個二進位位元組都會以2位數的十六進位數位表示）。|  
|SQL_TYPE_DATE|10（格式為*yyyy-mm-dd*的日期）。|  
|SQL_TYPE_TIME|8（格式為*hh： mm： ss*的時間）<br /><br /> - 或 -<br /><br /> 9 + *s* （格式為*hh： mm： ss*[. fff ...] 的時間，其中*s*是小數秒數精確度）。|  
|SQL_TYPE_TIMESTAMP|19（適用于*yyyy-dd hh： mm： ss*格式的時間戳記）<br /><br /> - 或 -<br /><br /> 20 + *s* （適用于*yyyy-mm-dd hh： mm： ss*[. fff ...] 格式的時間戳記，其中*s*是小數秒數精確度）。|  
|所有間隔資料類型|請參閱[Interval 資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36（ *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式的字元數|  
  
 [a] 如果驅動程式無法判斷變數類型的資料行或參數長度，就會傳回 SQL_NO_TOTAL。
