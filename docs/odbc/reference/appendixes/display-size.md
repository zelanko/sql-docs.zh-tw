---
description: 顯示大小
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 747c2076c528df8c312c9b3ed45e45a165299d59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456583"
---
# <a name="display-size"></a>顯示大小
資料行的顯示大小是以字元形式顯示資料所需的最大字元數。 下表定義每個 ODBC SQL 資料類型的顯示大小。  
  
|SQL 類型識別碼|顯示大小|  
|-------------------------|------------------|  
|所有字元類型 [a]|針對固定類型所定義的 () 或 (變數類型的最大值，) 以字元格式顯示資料所需的字元數。|  
|SQL_DECIMAL SQL_NUMERIC|資料行的有效位數加上 2 (正負號 *、有效位數和* 小數點) 。 例如，定義為數值 (10，3) 的資料行顯示大小為12。|  
|SQL_BIT|1 (1 位數) 。|  
|SQL_TINYINT|如果已簽署 (正負號和3位數，則為4，如果未簽署 (3 位數) ，則為3位數) |  
|SQL_SMALLINT|6如果簽署 (正負號和5位數) 或5（如果未簽署 (5 位數) 。|  
|SQL_INTEGER|11如果簽署 (正負號和10位數) 或10（如果未簽署 (10 位數）) 。|  
|SQL_BIGINT|20 (正負號或20位數的正負號（如果未簽署的) ，則為19位數。|  
|SQL_REAL|14 (正負號、7位數、小數點、字母 *E*、正負號和2位數) 。|  
|SQL_FLOAT SQL_DOUBLE|24 (正負號、15位數、小數點、字母 *E*、正負號和3位數) 。|  
|所有二進位類型 [a]|變數類型的已定義或最大 () 長度的資料行次2。  (每個二進位位元組都以2位數的十六進位數位表示。 ) |  
|SQL_TYPE_DATE|10 (格式為 *yyyy-mm-dd*) 的日期。|  
|SQL_TYPE_TIME|8 (時間，格式為 *hh： mm： ss*) <br /><br /> - 或 -<br /><br /> 9 + *s* (格式為 *hh： mm： ss*[...] 的時間，其中 *s* 是小數秒精確度) 。|  
|SQL_TYPE_TIMESTAMP|19 (*yyyy-mm-dd hh： mm： ss* 格式的時間戳記) <br /><br /> - 或 -<br /><br /> 20 + *s* (*yyyy-mm-dd hh： mm： ss*[...] 格式的時間戳記，其中 *s* 是小數秒精確度) 。|  
|所有間隔資料類型|請參閱 [間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36 (*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* 格式的字元數|  
  
 [a] 如果驅動程式無法判斷變數類型的資料行或參數長度，則會傳回 SQL_NO_TOTAL。
