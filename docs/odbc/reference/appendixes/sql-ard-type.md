---
title: SQL_ARD_TYPE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 683b81f82094aa33deef86ffc19dc8c5c0a53a27
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270440"
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
SQL_ARD_TYPE 型別識別項用來表示緩衝區中的資料將會 ARD SQL_DESC_CONCISE_TYPE 欄位中指定之類型。 中輸入 SQL_ARD_TYPE *TargetType*呼叫的引數**SQLGetData**而不是特定資料類型並可讓應用程式變更的資料緩衝區的輸入變更的描述元欄位。 這個值會繫結的資料型別 *\*TargetValuePtr*緩衝區描述項欄位。 (的呼叫中未輸入 SQL_ARD_TYPE **SQLBindCol**或是**SQLBindParameter**因為的繫結的緩衝區類型已經繫結至 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 欄位，而且可以變更隨時變更這些欄位。）  
  
 SQL_ARD_TYPE 型別識別項可以用來指定非預設值開頭的有效位數的秒數有效位數的間隔資料類型，並輸入 SQL_C_NUMERIC 資料的有效位數和小數位數的值。 如需詳細資訊，請參閱 <<c0> [ 覆寫預設前置和間隔資料類型的秒數有效位數](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)並[覆寫預設的有效位數和小數位數數字的資料類型](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)稍後在本附錄中。
