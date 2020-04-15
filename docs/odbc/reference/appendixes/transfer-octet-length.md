---
title: 傳輸八進位長度 |微軟文件
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4204b47816747506a5672241eeeef736eca54856
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302809"
---
# <a name="transfer-octet-length"></a>傳輸八位元長度
列的傳輸八字形長度是將數據傳輸到其預設 C 數據類型時返回給應用程式的最大位元組數。 對於字元數據,傳輸八字形長度不包括空終止字元的空間。 列的傳輸八進位長度可能與將數據存儲在數據源上所需的位元組數不同。  
  
 為每種 ODBC SQL 數據類型定義的傳輸八進位長度顯示在下表中。  
  
|SQL 類型識別碼|長度|  
|-------------------------|------------|  
|所有字元型別[a]|以位元組為單位的列的已定義或最大長度(對於變數類型)。 這與描述符欄位SQL_DESC_OCTET_LENGTH的值相同。|  
|SQL_DECIMAL<br />SQL_NUMERIC|如果字元集為 ANSI,則保存此資料的字元表示形式所需的位元組數;如果字元集為 UNICODE,則此數位為兩倍。 這是數位加上兩個的最大數位數,因為數據作為字串返回,數位、符號和小數點需要字元。 例如,定義為數位(10,3)的列的傳輸長度為 12。|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|所有二進位類型[a]|保存定義的(對於固定類型)或最大(對於變數類型)字元數所需的位元組數。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6(SQL_DATE_STRUCT或SQL_TIME_STRUCT結構的大小)。|  
|SQL_TYPE_TIMESTAMP|16 (SQL_TIMESTAMP_STRUCT結構的大小)。|  
|所有間隔資料型態|34 (間隔結構的大小)。|  
|SQL_GUID|16 (GUID 結構的大小)。|  
| &nbsp; | &nbsp; |

 [a] 如果驅動程式無法確定變數類型的列或參數長度,則返回SQL_NO_TOTAL。
