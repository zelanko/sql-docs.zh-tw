---
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
ms.openlocfilehash: d7e28d6babb7db8364697ae62092256396b44914
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305029"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 類型識別碼是用來指出緩衝區中的資料將會是 ARD 的 [SQL_DESC_CONCISE_TYPE] 欄位中所指定的類型。 SQL_ARD_TYPE 是在呼叫**SQLGetData** （而非特定資料類型）的*TargetType*引數中輸入，並可讓應用程式藉由變更描述元欄位來變更緩衝區的資料類型。 這個值會將* \*TargetValuePtr*緩衝區的資料類型與描述項欄位結合。 （SQL_ARD_TYPE 不會在呼叫**SQLBindCol**或**SQLBindParameter**時進入，因為系結緩衝區的類型已經系結至 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 欄位，而且可以隨時變更其中一個欄位來加以變更）。  
  
 SQL_ARD_TYPE 類型識別碼可以用來指定預設值，以取得間隔資料類型的前置精確度和秒精確度，以及 SQL_C_NUMERIC 資料類型的有效位數和小數位數值。 如需詳細資訊，請參閱本附錄稍後的覆[寫間隔資料類型的預設前置和秒](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)有效位數和覆[寫數值資料類型的預設精確度和小數位](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)數。
