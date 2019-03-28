---
title: 使用語意搜尋在文件中尋找主要片語 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], key phrase queries
ms.assetid: 6ee3676e-ed5d-43ec-aeca-1eed78967111
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 81b43a14a2410fc24bcc1bcd6968b9d87181cefa
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528480"
---
# <a name="find-key-phrases-in-documents-with-semantic-search"></a>使用語意搜尋找到文件中的主要片語
  描述如何在設定為統計語意索引的文件或文字資料行中尋找主要片語。  
  
##  <a name="BasicsQueryKey"></a> 在 文件中尋找主要片語  
  
###  <a name="howtofind"></a> 操作說明：使用 SEMANTICKEYPHRASETABLE 的文件中尋找主要片語  
 若要在特定文件中識別主要片語，或識別包含特定主要片語的文件，請查詢 [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql) 函數。  
  
 SEMANTICKEYPHRASETABLE 會傳回包含零個、一個或多個資料列的資料表，表示與指定之資料表資料行相關聯的主要片語。 您可以在 SELECT 陳述式的 FROM 子句中參考這個資料列集函數，就像是一般資料表名稱一樣。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，只有單一字會針對語意搜尋編制索引，多字片語 (ngrams) 則不會編制索引。 此外，相同字的不同形式會個別編制索引，例如 "computer" 和 "computers" 會個別編制索引。  
  
 如需 SEMANTICKEYPHRASETABLE 函數所需之參數及其傳回之結果資料表的詳細資訊，請參閱 [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)。  
  
> [!IMPORTANT]  
>  您設定為目標的資料行必須已啟用全文檢索和語意索引。  
  
###  <a name="HowToTopPhrases"></a> 範例 1：尋找在特定文件中的前幾個關鍵片語  
 下列範例會從 AdventureWorks 範例資料庫之 Production.Document 資料表 Document 資料行 @DocumentId 變數所指定的文件中，擷取前 10 個主要片語。 @DocumentId 變數是指來自全文檢索索引之索引鍵資料行的值。  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
GO  
```  
  
 **SEMANTICKEYPHRASETABLE** 函數會使用索引搜尋有效率地擷取這些結果，而不會使用資料表掃描。  
  
###  <a name="HowToTopDocuments"></a> 範例 2：找到包含特定關鍵片語的最上層文件  
 下列範例會從 AdventureWorks 範例資料庫 Production.Document 資料表的 Document 資料行中，擷取前 25 份包含主要片語的 "Bracket" 的文件。  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
GO  
```  
  
  
