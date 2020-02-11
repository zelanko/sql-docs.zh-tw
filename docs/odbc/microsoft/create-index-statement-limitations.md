---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ddb695d996cdd40b7fde4087799e5c1ec84224c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081936"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 陳述式限制
Microsoft Excel 或文字驅動程式不支援 CREATE INDEX 語句。  
  
 索引最多可以定義10個數據行。 如果 CREATE INDEX 語句中包含10個以上的資料行，將無法辨識索引，而且會將資料表視為未建立索引。  
  
 DBASE 驅動程式無法在邏輯資料行上建立索引。  
  
 使用 dBASE 驅動程式時，可以藉由在 SELECT 語句的 WHERE 子句中所指定的資料行（欄位）上建立 mdx （或 ndx）索引，來改善大型檔案的回應時間。 現有的。 mdx 索引將會自動套用至 WHERE 子句中\<的 =、>、、>=、=< 和運算子之間，以及 LIKE 述詞和聯結述詞中。  
  
 使用 dBASE 驅動程式時，建立唯一索引語句所建立的索引實際上不是唯一的，而且可以將重複的值插入索引資料行中。 只有具有相同索引鍵值之集合中的一筆記錄，才可以加入至索引。  
  
 使用 Paradox 驅動程式時，必須在資料表中連續的資料行子集上定義唯一索引，包括第一個資料行。 如果未在資料表上定義唯一索引，或使用 Paradox 驅動程式而未執行 Borland 資料庫引擎，Paradox 驅動程式就無法更新資料表。
