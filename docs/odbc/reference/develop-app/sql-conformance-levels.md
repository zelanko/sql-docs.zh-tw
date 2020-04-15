---
title: SQL 一致性級別 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 875330ac78588566b4b1c212f7a65d2841127a61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301379"
---
# <a name="sql-conformance-levels"></a>SQL 一致性層級
驅動程式支援的 SQL-92 語法級別由調用**SQLGetInfo**返回的值(具有SQL_SQL_CONFORMANCE資訊類型)指示。 這指示驅動程式是否符合 SQL-92 中定義的入口、FIPS 過渡、中間或完整級別。  
  
 所有 ODBC 驅動程式都必須支援附錄 C:SQL 語法中的[SQL 最小語法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)中描述的最小 SQL 語法。 此語法是 SQL-92 條目級別的子集。 驅動程式可能支援其他 SQL,並且符合 SQL-92 輸入、中間或完整級別,或符合 FIPS 127-2 過渡級別。 符合給定級別的 SQL-92 或 FIPS 127-2 的驅動程式可以支援任何較高級別的其他功能,但尚未完全符合該級別。 要確定是否支援某項功能,應用程式應使用適當的資訊類型調用**SQLGetInfo。** SQL 功能的一致性級別在相應的資訊類型中描述。 (請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明。
