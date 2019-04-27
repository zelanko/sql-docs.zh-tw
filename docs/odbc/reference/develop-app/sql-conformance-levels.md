---
title: SQL 一致性層級 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2e8ce5aeeb94a4f7a33b22054adc8067e0654ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690201"
---
# <a name="sql-conformance-levels"></a>SQL 一致性層級
驅動程式支援的 SQL-92 語法層級會由呼叫所傳回的值**SQLGetInfo** SQL_SQL_CONFORMANCE 資訊類型。 這表示驅動程式是否符合以 SQL-92 定義的項目，FIPS Transitional、 中級者、 或完整層級。  
  
 所有的 ODBC 驅動程式必須支援中所述的最低 SQL 文法[SQL 最小文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)附錄 c:SQL 文法。 此文法是 SQL-92 的項目層級的子集。 驅動程式可能支援其他的 SQL 和其符合標準的 SQL-92 項目、 中級者、 或 完整的層級，或 FIPS 127-2 過渡期的層級。 給定的層級，SQL-92 的 FIPS 127-2 符合的驅動程式可以支援任何更高的層級中的其他功能，但不能完全符合標準的程度。 若要判斷是否支援的功能，應用程式應該呼叫**SQLGetInfo**與適當的資訊類型。 SQL 功能的一致性層級描述中對應的資訊類型。 (請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。)
