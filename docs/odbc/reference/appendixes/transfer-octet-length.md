---
title: 傳輸八位元長度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8f64172685c42a5dde8de9027c8c7e621ddd9f2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601326"
---
# <a name="transfer-octet-length"></a>傳輸八位元長度
傳輸八位元長度的資料行是資料傳輸至其預設 C 資料類型時，應用程式傳回的位元組數目上限。 若是字元資料，傳輸八位元長度不包括 null 結束字元的空間。 傳輸八位元資料行的長度可能是不同的資料儲存在資料來源上所需的位元組數目。  
  
 傳輸八位元長度，為每個 ODBC SQL 資料類型定義下表所示。  
  
|SQL 型別識別項|長度|  
|-------------------------|------------|  
|所有字元類型 [a]|定義或資料行，以位元組為單位的長度上限 （適用於變數類型）。 這是描述項欄位的 SQL_DESC_OCTET_LENGTH 相同的值。|  
|SQL_DECIMAL<br />SQL_NUMERIC|保留字元表示法，此資料的字元集為 ANSI，如果所需的位元組數目，兩次這個數字的字元集是否為 UNICODE。 因為資料會傳回字元字串和字元所需的數字、 符號和小數點，這會是數字加上兩個的最大數目。 比方說，傳輸的資料行長度定義為 NUMERIC(10,3) 為 12。|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|保留字元表示法，此資料的字元集為 ANSI，如果所需的位元組數目，兩次此數字的字元集會是 UNICODE，因為此資料類型預設會傳回字元字串。 代表的字元是由 20 個字元所組成： 數字和符號，如果登入，或 20 位數，如果不帶正負號的 19。 因此，長度為 20。|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|所有的二進位類型 [a]|保留 （適用於固定類型） 的定義所需的位元組或字元數目上限 （適用於變數的型別） 的數目。|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 （SQL_DATE_STRUCT 或 SQL_TIME_STRUCT 結構的大小）。|  
|SQL_TYPE_TIMESTAMP|16 （SQL_TIMESTAMP_STRUCT 結構的大小）。|  
|間隔的所有資料類型|34 （間隔結構的大小）。|  
|SQL_GUID|16 （GUID 結構的大小）。|  
  
 [a] 如果驅動程式無法判斷變數類型的資料行或參數的長度，則會傳回 SQL_NO_TOTAL。
