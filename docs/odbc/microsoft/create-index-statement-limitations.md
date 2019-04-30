---
title: CREATE INDEX 陳述式限制 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ec6ba27197f7a6021aff90d30884129128cb3614
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232277"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 陳述式限制
Microsoft Excel 或文字的驅動程式不支援 CREATE INDEX 陳述式。  
  
 可以定義最多 10 個資料行索引。 如果在 CREATE INDEX 陳述式中包含超過 10 個資料行，則將無法辨識索引和資料表會被視為任何索引所建立。  
  
 DBASE 驅動程式無法在邏輯資料行上建立索引。  
  
 使用 dBASE 驅動程式時，可改善回應時間，大型檔案上的 SELECT 陳述式的 WHERE 子句中指定的資料行 （欄位） 上建置.mdx （或.ndx） 的索引。 現有的.mdx 索引將會自動套用而 =，>， \<，> =、 = <，及 BETWEEN 運算子在 WHERE 子句、 LIKE 述詞，以及聯結述詞。  
  
 使用 dBASE 驅動程式時，CREATE UNIQUE INDEX 陳述式所建立的索引實際上是非唯一的而且重複的值可以插入到索引的資料行。 從一組具有相同索引鍵值的只有一筆記錄可以加入至索引。  
  
 使用 Paradox 驅動程式時，必須定義唯一索引時的資料表，包括第一個資料行的資料行的連續子集。 Paradox 驅動程式無法更新資料表，如果針對資料表或 Paradox 驅動程式配合 Borland 資料庫引擎的實作未定義唯一索引。
