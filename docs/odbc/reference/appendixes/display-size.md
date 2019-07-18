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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130016"
---
# <a name="display-size"></a>顯示大小
資料行的顯示大小是以字元格式顯示資料所需字元數目上限。 下表定義每個 ODBC SQL 資料類型的顯示大小。  
  
|SQL 型別識別項|顯示大小|  
|-------------------------|------------------|  
|所有字元類型 [a]|定義 （適用於固定的型別） 或 （適用於變數的型別） 的最大字元形式來顯示資料所需的字元數。|  
|SQL_DECIMAL SQL_NUMERIC|資料行加上 2 的有效位數 (號、 一*精確度*數字和小數點)。 例如，定義為 NUMERIC(10,3) 的資料行的顯示大小為 12。|  
|SQL_BIT|1 （1 個數字）。|  
|SQL_TINYINT|如果簽章 （正負號和 3 個數字） 4 或 3，表示不帶正負號 （3 位數）。|  
|SQL_SMALLINT|如果登入 （登和 5 個數字） 的 6 或 5，如果不帶正負號 （5 個數字）。|  
|SQL_INTEGER|如果登入 （登和 10 個數字） 的 11 或 10，如果不帶正負號 （10 個數字）。|  
|SQL_BIGINT|20 （徵兆和 19 位數，如果簽章或 20 的數字，如果不帶正負號）。|  
|SQL_REAL|14 (符號、 7 位數、 小數點、 字母*E*，符號和 2 的數字)。|  
|SQL_FLOAT SQL_DOUBLE|24 (符號、 15 位數、 小數點、 字母*E*，符號，以及 3 位數)。|  
|所有的二進位類型 [a]|定義或 （適用於變數的型別） 的最大資料行長度逾 2。 （每個二進位的位元組被以 2 位數的十六進位數字。）|  
|SQL_TYPE_DATE|10 (格式的日期*yyyy-mm-dd 的-* )。|  
|SQL_TYPE_TIME|8 (時間格式*hh: mm:* )<br /><br /> - 或 -<br /><br /> 9 + *s* (時間格式*hh: mm:* [.fff...]，其中*s*小數秒數有效位數)。|  
|SQL_TYPE_TIMESTAMP|19 (針對在時間戳記*yyyy 為 yyyy-mm-dd hh: mm:* 格式)<br /><br /> - 或 -<br /><br /> 20 + *s* (針對在時間戳記*yyyy 為 yyyy-mm-dd hh: mm:* [.fff] 格式，其中*s*小數秒數有效位數)。|  
|間隔的所有資料類型|請參閱[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36 (中的字元數*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式|  
  
 [a] 如果驅動程式無法判斷資料行或參數的長度變數型別，它會傳回 SQL_NO_TOTAL。
