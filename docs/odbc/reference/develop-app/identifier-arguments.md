---
description: 識別碼引數
title: 識別碼引數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24efb295c9c27dbfc5edc2b1d7a46d6ca166e2c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461449"
---
# <a name="identifier-arguments"></a>識別碼引數
如果識別碼引數中的字串加上引號，驅動程式會移除開頭和尾端空白，並將字串視為引號內的字串。 如果字串未加上引號，驅動程式會移除尾端空白並將字串折迭為大寫。 將識別碼引數設定為 null 指標會傳回 SQL_ERROR 和 SQLSTATE HY009 (不正確使用 null 指標) ，除非引數是目錄名稱，且不支援目錄。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將這些引數視為識別碼引數。 在此情況下，會將底線 (_) 和百分比符號 (% ) 視為實際字元，而不是搜尋模式字元。 如果這個屬性設定為 SQL_FALSE，則會將這些引數視為一般引數或模式引數（視引數而定）。  
  
 雖然包含特殊字元的識別碼在 SQL 語句中必須以引號括住，但在當做類別目錄函式引數傳遞時，不能以引號括住，因為傳遞至目錄函式的引號字元實際上會被解讀 例如，假設 (的識別碼引號字元，它是驅動程式專屬的，而且透過 **SQLGetInfo**) 傳回 ( ") 的雙引號。 第一次呼叫 **SQLTables** 時，會傳回包含帳戶應付資料表相關資訊的結果集，而第二個呼叫則會傳回「帳戶應付」資料表的相關資訊，這可能不是預期的。  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 引號識別碼用來區別真正的資料行名稱與相同名稱的虛擬資料行，例如 Oracle 中的 ROWID。 如果在目錄函式的引數中傳遞「ROWID」，則函式會使用 ROWID 虛擬資料行（如果存在的話）。 如果虛擬資料行不存在，則函式會使用「ROWID」資料行。 如果在類別目錄函式的引數中傳遞 ROWID，此函數將會使用 ROWID 資料行。  
  
 如需引號識別碼的詳細資訊，請參閱 [引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。
