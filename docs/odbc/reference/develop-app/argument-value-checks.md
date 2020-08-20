---
description: 引數值檢查
title: 引數值檢查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5dac29eea6c9a2b5f178aa233520674ea466cf48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465950"
---
# <a name="argument-value-checks"></a>引數值檢查
驅動程式管理員會檢查下列類型的引數。 除非另有說明，否則驅動程式管理員會傳回引數值的錯誤 SQL_ERROR。  
  
-   環境、連接和語句的控制碼通常不能是 null 指標。 當驅動程式管理員找到 null 控制碼時，會傳回 SQL_INVALID_HANDLE。  
  
-   必要的指標引數（例如**SQLAllocHandle**中的*OutputHandlePtr*和**SQLSetCursorName**中的*CursorName* ）不可以是 null 指標。  
  
-   不支援驅動程式專用值的選項旗標必須是合法值。 例如，SQLSetPos*中*的**SQLSetPos**作業必須是 SQL_POSITION、SQL_REFRESH、SQL_UPDATE、SQL_DELETE 或 SQL_ADD。  
  
-   驅動程式支援的 ODBC 版本中必須支援選項旗標。 例如， **SQLGetInfo**中的*InfoType*無法 SQL_ASYNC_MODE 在呼叫 odbc 2.0 驅動程式時，于 odbc 3.0) 中引進的 (。  
  
-   根據函式而定，資料行和參數數目必須大於0或大於或等於0。 驅動程式必須根據目前的結果集或 SQL 語句，檢查這些引數值的上限。  
  
-   長度/指標引數和資料緩衝區長度引數必須包含適當的值。 例如，在**SQLColumns** (*NameLength3*) 中指定資料表名稱長度的引數必須 SQL_NTS 或大於0的值;**SQLDescribeCol**中的*BufferLength*必須大於或等於0。 驅動程式可能也需要檢查這些引數。 例如，它可能會檢查 *NameLength3* 是否小於或等於資料來源中資料表名稱的最大長度。
