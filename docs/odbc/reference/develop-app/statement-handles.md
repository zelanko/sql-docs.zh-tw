---
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
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299674"
---
# <a name="statement-handles"></a>陳述式控制代碼
*語句*最容易被視為 SQL 語句，例如** \* SELECT FROM Employee**。 不過，語句不只是 SQL 語句，它包含與該 SQL 語句相關聯的所有資訊，例如語句所建立的任何結果集，以及執行語句時所使用的參數。 語句甚至不需要有應用程式定義的 SQL 語句。 例如，當在語句上執行諸如**SQLTables**之類的目錄函數時，它會執行可傳回資料表名稱清單的預先定義 SQL 語句。  
  
 每個語句都是由語句控制碼所識別。 語句與單一連接相關聯，而且該連接上可以有多個語句。 有些驅動程式會限制它們所支援的使用中語句數目;**SQLGetInfo**中的 SQL_MAX_CONCURRENT_ACTIVITIES 選項會指定在單一連接上，驅動程式支援多少使用中語句。 如果語句具有暫止的結果，且其結果為結果集或受**INSERT**、 **UPDATE**或**DELETE**語句影響的資料列計數，或正在使用**SQLPutData**的多個呼叫傳送資料，則語句會*定義為使用*中。  
  
 在執行 ODBC （驅動程式管理員或驅動程式）的程式碼片段內，語句控制碼會識別包含語句資訊的結構，例如：  
  
-   語句的狀態  
  
-   目前的語句層級診斷  
  
-   系結至語句參數和結果集資料行之應用程式變數的位址  
  
-   每個語句屬性的目前設定  
  
 語句控制碼用於大部分的 ODBC 函式中。 值得注意的是，它們會在函式中用來系結參數和結果集資料行（**SQLBindParameter**和**SQLBindCol**）、準備和執行語句（**SQLPrepare**、 **SQLExecute**和**SQLExecDirect**）、取出中繼資料（**SQLColAttribute**和**SQLDescribeCol**）、提取結果（**SQLFetch**），以及取得診斷（**SQLGetDiagField**和**SQLGetDiagRec**）。 它們也會用於目錄函式（**SQLColumns**、 **SQLTables**等等）和許多其他函數。  
  
 語句控制碼會使用**SQLAllocHandle**配置，並與**SQLFreeHandle**一起釋放。
