---
description: CREATE INDEX 陳述式限制
title: CREATE INDEX 語句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db2b346afa13e7f7f37151d6d4fa8efdca9fa230
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466450"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 陳述式限制
Microsoft Excel 或文字驅動程式不支援 CREATE INDEX 語句。  
  
 最多可以定義10個數據行的索引。 如果 CREATE INDEX 語句中包含10個以上的資料行，將無法辨識索引，而且會將資料表視為未建立索引。  
  
 DBASE 驅動程式無法在邏輯資料行上建立索引。  
  
 使用 dBASE 驅動程式時，您可以在 SELECT 語句的 WHERE 子句中指定的資料行 (欄位)  (或 ndx) 索引，來改善大型檔案的回應時間。 現有的. mdx 索引會自動套用至 WHERE 子句中的 =、>、 \<, > =、=< 和運算子之間，以及 WHERE 子句中的運算子和聯結述詞。  
  
 使用 dBASE 驅動程式時，CREATE UNIQUE INDEX 語句所建立的索引實際上不是唯一的，而且可以在索引資料行中插入重複的值。 只有一個具有相同索引鍵值之集合的記錄可以加入至索引。  
  
 使用 Paradox 驅動程式時，必須在資料表中連續的資料行子集（包括第一個資料行）上定義唯一索引。 如果未在資料表上定義唯一索引，或在未執行 Borland 資料庫引擎的情況下使用 Paradox 驅動程式時，Paradox 驅動程式就無法更新資料表。
