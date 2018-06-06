---
title: 傳輸八位元長度 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 157dbea8954dd7823888360c7d9cf74d9c8db74d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="transfer-octet-length"></a>傳輸八位元長度
傳輸八位元長度的資料行是資料轉送到其預設 C 資料類型時，應用程式傳回的位元組數目上限。 字元資料傳輸八位元長度不包含 null 結束字元的空間。 資料行的傳輸八位元長度可能不同於資料儲存在資料來源上所需的位元組數目。  
  
 下表顯示每個 ODBC SQL 資料類型所定義的傳輸八位元長度。  
  
|SQL 類型識別碼|長度|  
|-------------------------|------------|  
|所有的字元類型 [a]|定義或資料行，以位元組為單位的長度上限 （適用於變數類型）。 這是描述項欄位 SQL_DESC_OCTET_LENGTH 相同的值。|  
|SQL_DECIMAL<br />SQL_NUMERIC|保留的字元表示法，這項資料的字元集為 ANSI，如果所需的位元組數目以及兩次此數字的字集是否為 UNICODE。 這是數字加上兩個，最大數目，因為做為字元字串所傳回的資料，以及字元所需的數字、 符號和小數點。 例如，資料行定義為 NUMERIC(10,3) 傳輸長度為 12。|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|如果字元資料集為 ANSI，保留的字元表示法，這項資料的所需的位元組數目以及兩次此數字如果字元是 UNICODE，因為此資料類型預設會傳回做為字元字串。 字元表示法包含 20 個字元： 數字和符號，如果登入或 20 位數，如果不帶正負號為 19。 因此，長度為 20。|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|所有二進位型別 [a]|保留 （適用於固定類型） 的定義所需的位元組或 （適用於變數類型） 的最大字元數的數目。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 （SQL_DATE_STRUCT 或 SQL_TIME_STRUCT 結構的大小）。|  
|SQL_TYPE_TIMESTAMP|16 （SQL_TIMESTAMP_STRUCT 結構的大小）。|  
|所有的間隔資料型別|34 （間隔結構的大小）。|  
|SQL_GUID|16 （使用 GUID 結構的大小）。|  
  
 [a] 如果驅動程式無法判斷變數類型的資料行或參數的長度，則會傳回 SQL_NO_TOTAL。
