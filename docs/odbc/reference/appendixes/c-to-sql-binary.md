---
title: C 到 SQL：二進位 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818de0086ce3996cc1f6194311d2a2bb80c9f564
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292114"
---
# <a name="c-to-sql-binary"></a>C 到 SQL：二進位
Binary ODBC C 資料類型的識別碼為：  
  
 SQL_C_BINARY  
  
 下表顯示二進位 C 資料可能轉換成的 ODBC SQL 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 類型識別碼|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Data <的位元組長度 = 資料行位元組長度<br /><br /> 資料行位元組長度的位元組長度 >|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|<的字元長度 = 資料行字元長度<br /><br /> 資料行字元長度 > 的字元長度|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|資料的位元組長度 = SQL 資料長度<br /><br /> 資料的位元組長度 <> SQL 資料長度|n/a<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|資料長度 <= 資料行長度<br /><br /> 資料 > 資料行長度的長度|n/a<br /><br /> 22001|
