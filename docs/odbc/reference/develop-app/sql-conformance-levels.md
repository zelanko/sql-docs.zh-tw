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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 875330ac78588566b4b1c212f7a65d2841127a61
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301379"
---
# <a name="sql-conformance-levels"></a>SQL 一致性層級
驅動程式支援的 SQL-92 文法層級是以 SQL_SQL_CONFORMANCE 資訊類型呼叫**SQLGetInfo**所傳回的值來表示。 這會指出驅動程式是否符合 SQL-92 中所定義的專案、FIPS 過渡、中繼或完整層級。  
  
 所有 ODBC 驅動程式都必須支援附錄 C： SQL 文法中的[Sql 最低文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)中所述的最小 sql 文法。 此文法是 SQL-92 進入層級的子集。 驅動程式可能會支援額外的 SQL，並符合 SQL-92 專案、中繼或完整層級，或 FIPS 127-2 轉換層級。 符合特定 SQL-92 或 FIPS 127-2 層級的驅動程式可以支援任何較高等級的其他功能，但不完全符合該層級。 若要判斷是否支援某個功能，應用程式應該呼叫具有適當資訊類型的**SQLGetInfo** 。 SQL 功能的一致性層級會在對應的資訊類型中說明。 （請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述）。
