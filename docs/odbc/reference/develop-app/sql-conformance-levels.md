---
description: SQL 一致性層級
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
ms.openlocfilehash: 525cda9094213e6decf30643c23a7db623511e14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499801"
---
# <a name="sql-conformance-levels"></a>SQL 一致性層級
驅動程式支援的 SQL-92 文法層級 **是以 SQL_SQL_CONFORMANCE** 資訊類型的呼叫所傳回的值來表示。 這會指出驅動程式是否符合 SQL-92 中定義的專案、FIPS 轉換、中繼或完整層級。  
  
 所有 ODBC 驅動程式都必須支援附錄 C： SQL 文法中 [Sql 最低文法](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 所述的最小 sql 文法。 此文法是 SQL-92 專案層級的子集。 驅動程式可能會支援其他 SQL，並符合 SQL-92 專案、中繼或完整層級，或是 FIPS 127-2 過渡層級。 符合指定之 SQL-92 或 FIPS 127-2 層級的驅動程式可支援任何較高層級的其他功能，但不完全符合該層級。 若要判斷是否支援某項功能，應用程式應該使用適當的資訊類型來呼叫 **SQLGetInfo** 。 SQL 功能的一致性層級會在對應的資訊類型中描述。  (參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函式描述。 ) 
