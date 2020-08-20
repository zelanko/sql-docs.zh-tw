---
description: 陳述式控制代碼
title: 語句控制碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a93bdd42acccdca0563edc4104734d04522e7879
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476340"
---
# <a name="statement-handles"></a>陳述式控制代碼
*語句*最容易被視為 SQL 語句，例如**SELECT \* FROM Employee**。 不過，語句不只是 SQL 語句，它是由與該 SQL 語句相關聯的所有資訊所組成，例如語句所建立的任何結果集，以及執行語句所使用的參數。 語句甚至不需要有應用程式定義的 SQL 語句。 例如，在語句上執行類別目錄函數（例如 **SQLTables** ）時，它會執行預先定義的 SQL 語句，以傳回資料表名稱清單。  
  
 每個語句都是由語句控制碼來識別。 語句與單一連接相關聯，而且該連接上可以有多個語句。 某些驅動程式會限制它們支援的現用語句數目; **SQLGetInfo** 中的 SQL_MAX_CONCURRENT_ACTIVITIES 選項會指定驅動程式在單一連接上支援多少作用中語句。 如果語句有暫止的結果，語句 *會被定義* 為使用中，其中的結果會是結果集或受 **INSERT**、 **UPDATE**或 **DELETE** 語句影響的資料列計數，或者資料會透過多個呼叫 **SQLPutData**來傳送。  
  
 在處理 ODBC (驅動程式管理員或驅動程式) 的程式碼內，語句控制碼會識別包含語句資訊的結構，例如：  
  
-   語句的狀態  
  
-   目前的語句層級診斷  
  
-   系結至語句參數和結果集資料行的應用程式變數位址  
  
-   每個語句屬性的目前設定  
  
 語句控制碼用於大部分的 ODBC 函數。 值得注意的是，這些函數可用於系結參數和結果集資料行 (**SQLBindParameter** 和 **SQLBindCol**) 、prepare 和 execute 語句 (**SQLPrepare**、 **SQLExecute**和 **SQLExecDirect**) 、取出中繼資料 (**SQLColAttribute** 和 **SQLDescribeCol**) 、提取結果 (**SQLFetch) ，** 以及取得診斷 (**SQLGetDiagField** 和 **SQLGetDiagRec**) 。 它們也會用於目錄函式 (**SQLColumns**、 **SQLTables**等) 和一些其他函式。  
  
 語句控制碼會使用 **SQLAllocHandle** 進行配置，並使用 **SQLFreeHandle**來釋放。
