---
description: 語意搜尋 (SQL Server)
title: 語意搜尋 (SQL Server) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 8da5b57c26ad2b99ab11b058b9d3362ff48569e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490525"
---
# <a name="semantic-search-sql-server"></a>語意搜尋 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 統計語意搜尋會擷取統計上相關的「關鍵片語」** 並建立其索引，藉以深入解析儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的非結構化文件。 接著使用這些主要片語來識別「相似或相關文件」**，並建立其索引。  
  
##  <a name="what-can-you-do-with-semantic-search"></a><a name="whatcanido"></a> 可以使用語意搜尋進行哪些作業？  
 雖然語意搜尋是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中現有的全文檢索搜尋功能為建立基礎，但是可以實現超過關鍵字搜尋的新案例。 全文檢索搜尋可讓您查詢文件中的「字詞」**，而語意搜尋則可讓您查詢文件的「意義」**。 目前可能的方案包含自動標記擷取、相關內容探索，以及相似內容的階層式導覽。 例如，您可以查詢主要片語的索引來建立組織或文件主體的分類。 或者，您可以查詢文件相似度索引來識別符合工作描述的履歷表。  
  
 下列各範例示範語意搜尋的功能。 同時，這些範例示範用來查詢語意索引並以結構化資料形式擷取結果的三個 Transact-SQL 資料列集函式。  
  
###  <a name="find-the-key-phrases-in-a-document"></a><a name="find1"></a> 文件中尋找主要片語  
 下列查詢會取得範例文件中已識別的主要片語。 它會依照排列每個主要片語之統計重要性次序的分數，以遞減順序呈現結果。
 
 此查詢會呼叫 [semantickeyphrasetable](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md) 函式。  
  
```sql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
###  <a name="find-similar-or-related-documents"></a><a name="find2"></a> Find similar or related documents  
 下列查詢會取得識別為與範例文件相似或相關的文件。 它會依照排列這兩份文件之相似度次序的分數，以遞減順序呈現結果。
 
 此查詢會呼叫 [semanticsimilaritytable](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md) 函式。  
  
```vb  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS SourceTitle, DocumentTitle AS MatchedTitle,  
        DocumentID, score  
    FROM SEMANTICSIMILARITYTABLE(Documents, *, @DocID)  
    INNER JOIN Documents ON DocumentID = matched_document_key  
    ORDER BY score DESC  
  
```  
  
###  <a name="find-the-key-phrases-that-make-documents-similar-or-related"></a><a name="find3"></a> 尋找讓文件相似或相關的主要片語  
 下列查詢會取得讓兩份範例文件相似或相關的主要片語。 它會依照排列每個主要片語之加權次序的分數，以遞減順序呈現結果。
 
 此查詢會呼叫 [semanticsimilaritydetailstable](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md) 函式。  
  
```sql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
##  <a name="store-your-documents-in-sql-server"></a><a name="store"></a> 在 SQL Server 中儲存文件  
 在您使用語意搜尋索引文件前，必須先將文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中。  
  
 SQL Server 中的 FileTable 功能可讓非結構化檔案和文件成為關聯式資料庫的首要成員。 因此，資料庫開發人員可以在 Transact-SQL 集合式作業中，操作文件以及結構化資料。  
  
 如需 FileTable 功能的詳細資訊，請參閱 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。 如需 FILESTREAM 功能 (這是將文件儲存至資料庫的另一個選擇) 的詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)。  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> Related tasks  
 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)  
 描述統計語意搜尋的必要元件以及如何安裝或檢查這些必要元件。  
  
 [在資料表和資料行上啟用語意搜尋](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)  
 描述如何針對包含文件或文字的選取資料行啟用或停用統計語意索引。  
  
 [使用語意搜尋找到文件中的主要片語](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)  
 描述如何在設定為統計語意索引的文件或文字資料行中尋找主要片語。  
  
 [使用語意搜尋尋找相似及相關的文件](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)  
 描述如何在設定進行統計語意索引的資料行中尋找相似或相關的文件或文字值，以及相似或相關程度的詳細資訊。  
  
 [管理及監視語意搜尋](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
 描述語意索引的程序以及與監視及管理索引相關的工作。  
  
##  <a name="related-content"></a><a name="relcontent"></a> Related content  
 [語意搜尋 DDL、函數、預存程序及檢視](../../relational-databases/search/semantic-search-ddl-functions-stored-procedures-and-views.md)  
 列出加入或變更以支援統計語意搜尋的 Transact-SQL 陳述式和 SQL Server 資料庫物件。  
  
  
