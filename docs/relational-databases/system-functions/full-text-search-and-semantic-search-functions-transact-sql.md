---
description: 全文檢索搜尋與語意搜尋函數 (Transact-SQL)
title: " (Transact-sql) 的全文檢索搜尋和語義搜尋函數 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: deb790da4e4e263318717c3ee81cc8ee8d467ae6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474629"
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>全文檢索搜尋與語意搜尋函數 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本節說明全文檢索搜尋及語意搜尋相關的系統函數。  
  
## <a name="full-text-search-functions"></a>全文檢索搜尋函數  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 針對包含完全或部分 (較不精確) 符合單一字詞及片語、字詞彼此之間的相似程度或加權相符的資料行，傳回包含零個、一個或多個資料列的資料表。  
  
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 傳回零個、一個或多個資料列的資料表，這些資料行包含的值符合指定之 *freetext_string*中文字的意義，而不只是確切的用語。  
  
## <a name="semantic-search-functions"></a>語意搜尋函數  
 [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 傳回零個、一個或多個資料列的資料表，表示與指定之資料表資料行相關聯的主要片語。  
  
 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 傳回零個、一個或多個資料列的資料表，表示內容為語義類似的兩個文件(來源文件和比對文件) 之間的共同關鍵片語。  
  
 [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 傳回零個、一個或多個資料列的資料表，表示內容與指定之文件語義類似的資料行。  
  
  
