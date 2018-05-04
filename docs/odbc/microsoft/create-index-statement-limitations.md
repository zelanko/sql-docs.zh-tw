---
title: 建立索引陳述式的限制 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d473a0fce55688dfa00fd916c5eab15bd4ad44e2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-index-statement-limitations"></a>建立索引陳述式的限制
Microsoft Excel 或文字的驅動程式不支援 CREATE INDEX 陳述式。  
  
 索引可以在最多 10 個資料行定義。 如果超過 10 個資料行包含在 CREATE INDEX 陳述式，將無法辨識索引和資料表會被視為所建立的任何索引。  
  
 DBASE 驅動程式無法建立索引的邏輯資料行上。  
  
 使用 dBASE 驅動程式時，來建立資料行 （欄位） 的 SELECT 陳述式的 WHERE 子句中指定.mdx （或.ndx） 索引可改善大型檔案上的回應時間。 現有的.mdx 索引就會自動套用 for =，>， \<，> =、 = <，及 BETWEEN 運算子，在 WHERE 子句、 LIKE 述詞，以及聯結述詞。  
  
 使用 dBASE 驅動程式時，CREATE UNIQUE INDEX 陳述式所建立的索引實際上是非唯一的且重複的值可以插入到索引的資料行。 只有一筆記錄，從一組具有相同索引鍵的值可以加入至索引。  
  
 使用 Paradox 驅動程式時，必須定義唯一索引時連續包括第一個資料行之資料表中的資料行的子集。 如果唯一的索引未定義的資料表，或 Borland 資料庫引擎的實作情況下使用 Paradox 驅動程式時，無法更新資料表 Paradox 驅動程式。
