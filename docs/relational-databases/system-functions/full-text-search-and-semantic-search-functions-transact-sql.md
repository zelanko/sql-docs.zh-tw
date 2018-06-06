---
title: 全文檢索搜尋和語意搜尋函數 (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 04356970f56a3a2e5ee8f2a824b722801fe7262a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>全文檢索搜尋與語意搜尋函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本節說明全文檢索搜尋及語意搜尋相關的系統函數。  
  
## <a name="full-text-search-functions"></a>全文檢索搜尋函數  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 針對包含完全或部分 (較不精確) 符合單一字詞及片語、字詞彼此之間的相似程度或加權相符的資料行，傳回包含零個、一個或多個資料列的資料表。  
  
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 傳回零個、 一個或多個資料列，這些資料行包含值符合意義，而且不只是完全相同，文字方塊中指定的資料表*freetext_string*。  
  
## <a name="semantic-search-functions"></a>語意搜尋函數  
 [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 傳回零個、一個或多個資料列的資料表，表示與指定之資料表資料行相關聯的主要片語。  
  
 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 傳回零個、一個或多個資料列的資料表，表示內容為語義類似的兩個文件(來源文件和比對文件) 之間的共同關鍵片語。  
  
 [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 傳回零個、一個或多個資料列的資料表，表示內容與指定之文件語義類似的資料行。  
  
  
