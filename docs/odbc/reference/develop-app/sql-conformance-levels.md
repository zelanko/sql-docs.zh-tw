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
ms.openlocfilehash: 7862b2e3a86c6d98a51c73ecb470d59bcfe29dc9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107526"
---
# <a name="sql-conformance-levels"></a>SQL 一致性層級
驅動程式支援的 SQL-92 文法層級是以 SQL_SQL_CONFORMANCE 資訊類型呼叫**SQLGetInfo**所傳回的值來表示。 這會指出驅動程式是否符合 SQL-92 中所定義的專案、FIPS 過渡、中繼或完整層級。  
  
 所有 ODBC 驅動程式都必須支援附錄 C： SQL 文法中的[Sql 最低文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)中所述的最小 sql 文法。 此文法是 SQL-92 進入層級的子集。 驅動程式可能會支援額外的 SQL，並符合 SQL-92 專案、中繼或完整層級，或 FIPS 127-2 轉換層級。 符合特定 SQL-92 或 FIPS 127-2 層級的驅動程式可以支援任何較高等級的其他功能，但不完全符合該層級。 若要判斷是否支援某個功能，應用程式應該呼叫具有適當資訊類型的**SQLGetInfo** 。 SQL 功能的一致性層級會在對應的資訊類型中說明。 （請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述）。
