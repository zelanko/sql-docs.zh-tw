---
title: SQL_ARD_TYPE |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7e28d6babb7db8364697ae62092256396b44914
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305029"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
SQL_ARD_TYPE類型標識符用於指示緩衝區中的數據將屬於 ARD SQL_DESC_CONCISE_TYPE 欄位中指定的類型。 SQL_ARD_TYPE在調用**SQLGetData**而不是特定資料類型的*TargetType*參數中輸入,並使應用程式能夠透過更改描述符欄位來更改緩衝區的數據類型。 此值將*\*TargetValuePtr*緩衝區的數據類型與描述符欄位進行關係。 (SQL_ARD_TYPE不會在調用**SQLBindCol**或**SQLBind 參數**時輸入,因為綁定緩衝區的類型已綁定到SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE欄位,並且可以隨時通過更改這些欄位中的任何一個進行更改。  
  
 SQL_ARD_TYPE類型識別碼可用於為間隔資料類型的前導精度和秒精度指定非預設值,以及SQL_C_NUMERIC資料類型的精度和縮放值。 有關詳細資訊,請參閱本附錄後面的[間隔數據類型](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)和[超值預設精度和「數位數據類型的覆蓋預設精度」和「覆蓋預設精度」和](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)「覆蓋」精度。
