---
description: SQL_ARD_TYPE
title: SQL_ARD_TYPE |Microsoft Docs
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
ms.openlocfilehash: 826b5aa2ff103a2c2868a6bc1dc09fb8cad40382
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483161"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 類型識別碼可用來表示緩衝區中的資料將會是 ARD 之 SQL_DESC_CONCISE_TYPE 欄位中所指定的類型。 在**SQLGetData**呼叫的*TargetType*引數中輸入 SQL_ARD_TYPE，而不是特定資料類型，並可讓應用程式藉由變更描述項欄位來變更緩衝區的資料類型。 此值會將* \* TargetValuePtr*緩衝區的資料類型系結至描述項欄位。 未在 **SQLBindCol** 或 **SQLBindParameter** 的呼叫中輸入 (SQL_ARD_TYPE，因為系結緩衝區的型別已系結至 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 欄位，而且可以隨時變更其中一個欄位來變更。 )   
  
 SQL_ARD_TYPE 類型識別碼可以用來指定非預設值，以用於間隔資料類型的前置精確度和秒有效位數，以及 SQL_C_NUMERIC 資料類型的有效位數和小數位數值。 如需詳細資訊，請參閱本附錄稍後的覆 [寫間隔資料類型的預設前置和秒](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) 有效位數，以及覆 [寫數值資料類型的預設精確度和小數位](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)數。
