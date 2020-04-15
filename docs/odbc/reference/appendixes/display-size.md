---
title: 顯示大小 |微軟文件
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
ms.openlocfilehash: 578bf0cbdf2dd1dbd06dd4a248f4efa5eb839916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307029"
---
# <a name="display-size"></a>顯示大小
列的顯示大小是以字元形式顯示數據所需的最大字元數。 下表定義了每種 ODBC SQL 資料類型的顯示大小。  
  
|SQL 類型識別碼|顯示大小|  
|-------------------------|------------------|  
|所有字元型別[a]|以字元形式顯示數據所需的已定義(對於固定類型)或最大(對於變數類型)的字元數。|  
|SQL_DECIMALSQL_NUMERIC|列加 2 的精度(符號、*精度*數位和小數點)。 例如,定義為數位(10,3)的列的顯示大小為 12。|  
|SQL_BIT|1(1 位)。|  
|SQL_TINYINT|4,如果簽名(一個符號和3位數位)或3,如果無符號(3位)。|  
|SQL_SMALLINT|6,如果簽名(一個符號和5位數位)或5,如果無符號(5位)。|  
|SQL_INTEGER|11 如果簽名(一個符號和 10 位元數位)或 10(未簽名(10 位)。|  
|SQL_BIGINT|20(簽名時為符號和19位數位,如果簽名則為20位數位(如果未簽名)。|  
|SQL_REAL|14(一個符號,7位數位,一個小數點,字母*E,* 一個符號和2位)。|  
|SQL_FLOATSQL_DOUBLE|24(一個符號,15位數位,一個小數點,字母*E,* 一個符號和3位數位)。|  
|所有二進位類型[a]|列的已定義或最大長度(對於變數類型)長度乘以 2。 (每個二進位位元組由2位十六進位數位表示。|  
|SQL_TYPE_DATE|10 (格式*yyyy-mm-dd*中的日期)。|  
|SQL_TYPE_TIME|8 (格式*hh:mm:sss 的時間*)<br /><br /> - 或 -<br /><br /> 9 = *s(* 格式*hh:mm:ss*[.fff...]的時間,其中*s*是小數秒精度)。|  
|SQL_TYPE_TIMESTAMP|19 (對於*yyyy-mm-dd hh:mm:ss*格式的時間戳)<br /><br /> - 或 -<br /><br /> 20 ° *s* (對於*yyyy-mm-dd hh:mm:ss*[.fff...] 格式的時間戳,其中*s*是小數秒精度)。|  
|所有間隔資料型態|請參考[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36 *(aaaaaaa-bbbb-cccc-ddd-eeeeeeeeeeeee*格式的字元數|  
  
 [a] 如果驅動程式無法確定變數類型的列或參數長度,則返回SQL_NO_TOTAL。
