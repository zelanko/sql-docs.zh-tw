---
title: C 到 SQL： 時間 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ea11803847505698ea42d13727b6177f3a24bda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606176"
---
# <a name="c-to-sql-time"></a>C 到 SQL：時間
時間 ODBC C 資料類型的識別項是：  
  
 SQL_C_TYPE_TIME  
  
 下表顯示 ODBC SQL 時間 C 資料可能會轉換成的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
|SQL 型別識別項|測試|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|資料行的位元組長度 > = 8<br /><br /> 資料行的位元組長度 < 8<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|資料行的字元長度 > = 8<br /><br /> 資料行的字元長度 < 8<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|資料值為有效的時間<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|資料值為有效的時間 [a]<br /><br /> 資料值不是有效的時間|n/a<br /><br /> 22007|  
  
 [a] 部分的時間戳記設為目前日期和時間戳記部分已設定為零的小數秒的日期。  
  
 如需哪些值是有效 SQL_C_TYPE_TIME 結構中的資訊，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)稍早在本附錄中。  
  
 當時間 C 資料轉換成字元 SQL 資料時，產生的字元資料是在 「*hh*:*mm*:*ss*」 格式。  
  
 從 C 資料類型，並假設資料緩衝區的大小，是時間 C 資料類型大小的時間轉換的資料時，驅動程式就會忽略長度/指標值。 傳入的長度/指標值無效*Strlen_or_ind&lt*中的引數**SQLPutData**並使用指定的緩衝區中*StrLen_or_IndPtr*引數中**SQLBindParameter**。 使用指定的資料緩衝區*DataPtr*中的引數**SQLPutData**並*ParameterValuePtr*中的引數**SQLBindParameter**.
