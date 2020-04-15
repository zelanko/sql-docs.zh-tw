---
title: 建立索引語句限制 |微軟文件
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
ms.openlocfilehash: 053287d5087b377429221c31dd4e6b20f24248e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280879"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX 陳述式限制
Microsoft Excel 或文本驅動程式不支援創建索引語句。  
  
 索引最多可以在 10 列上定義。 如果 CREATE INDEX 語句中包含超過 10 列,則無法識別索引,並且表將被視為未創建索引。  
  
 dBASE 驅動程式無法在「邏輯」列上創建索引。  
  
 使用 dBASE 驅動程式時,可以透過在 SELECT 語句的 WHERE 子句中指定的列(欄位)上生成 .mdx(或 .ndx) 索引來提高大型檔的回應時間。 現有 .mdx 索引將自動應用於 WHERE\<子句和 LIKE 謂詞中的 *、>、>*、*<和"關係運算符"以及聯接謂詞。  
  
 使用 dBASE 驅動程式時,由 CREATE UNIQUE INDEX 語句創建的索引實際上非唯一,重複值可以插入到索引列中。 只能將具有相同鍵值的集中的一條記錄添加到索引中。  
  
 使用 Paradox 驅動程式時,必須在表中列的連續子集(包括第一列)上定義唯一索引。 如果在表上未定義唯一索引,或者在沒有實現 Borland 資料庫引擎的情況下使用 Paradox 驅動程式時,悖論驅動程式無法更新表。
