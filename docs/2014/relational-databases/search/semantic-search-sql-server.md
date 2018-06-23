---
title: 語意搜尋 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8746a7f7a7fb8c1dfc84f3f50a09476f77b3c78a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137034"
---
# <a name="semantic-search-sql-server"></a>語意搜尋 (SQL Server)
  統計語意搜尋會擷取統計上相關的「主要片語」並建立其索引，藉以深入解析儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的非結構化文件。 然後，它也會使用這些主要片語來識別「相似或相關文件」，並建立其索引。  
  
 使用三個 Transact-SQL 資料列集函數，以結構化資料形式擷取結果，就可以查詢這些語意索引。  
  
##  <a name="whatcanido"></a> 可以做什麼使用語意搜尋？  
 雖然語意搜尋是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中現有的全文檢索搜尋功能為建立基礎，但是可以實現超過關鍵字搜尋的新案例。 全文檢索搜尋可讓您查詢文件中的「字詞」，而語意搜尋則可讓您查詢文件的「意義」。 目前可能的方案包含自動標記擷取、相關內容探索，以及相似內容的階層式導覽。 例如，您可以查詢主要片語的索引來建立組織或文件主體的分類。 或者，您可以查詢文件相似度索引來識別符合工作描述的履歷表。  
  
 下列各範例示範語意搜尋的功能。  
  
###  <a name="find1"></a> 文件中尋找主要片語  
 下列查詢會取得範例文件中已識別的主要片語。 它會依照排列每個主要片語之統計重要性次序的分數，以遞減順序呈現結果。 此查詢會呼叫 [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql) 函數。  
  
```tsql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
  
  
###  <a name="find2"></a> 尋找相似或相關文件  
 下列查詢會取得識別為與範例文件相似或相關的文件。 它會依照排列這兩份文件之相似度次序的分數，以遞減順序呈現結果。 此查詢會呼叫 [semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql) 函數。  
  
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
  
  
  
###  <a name="find3"></a> 尋找讓文件相似或相關的主要片語  
 下列查詢會取得讓兩份範例文件相似或相關的主要片語。 它會依照排列每個主要片語之加權次序的分數，以遞減順序呈現結果。 此查詢會呼叫 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql) 函數。  
  
```tsql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
  
  
##  <a name="store"></a> 在 SQL Server 中儲存的文件  
 在您使用語意搜尋索引文件前，必須先將文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的 FileTable 功能可讓非結構化檔案和文件成為關聯式資料庫的首要成員。 因此，資料庫開發人員可以在 Transact-SQL 集合式作業中，操作文件以及結構化資料。  
  
 如需有關 FileTable 功能的詳細資訊，請參閱 [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md)。 如需有關 FILESTREAM 功能 (這是將文件儲存至資料庫的另一個選擇) 的詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md)。  
  
  
  
##  <a name="reltasks"></a> 相關工作  
 [安裝及設定語意搜尋](install-and-configure-semantic-search.md)  
 描述統計語意搜尋的必要元件以及如何安裝或檢查這些必要元件。  
  
 [在資料表和資料行上啟用語意搜尋](enable-semantic-search-on-tables-and-columns.md)  
 描述如何針對包含文件或文字的選取資料行啟用或停用統計語意索引。  
  
 [使用語意搜尋找到文件中的主要片語](find-key-phrases-in-documents-with-semantic-search.md)  
 描述如何在設定為統計語意索引的文件或文字資料行中尋找主要片語。  
  
 [使用語意搜尋尋找相似及相關的文件](find-similar-and-related-documents-with-semantic-search.md)  
 描述如何在設定進行統計語意索引的資料行中尋找相似或相關的文件或文字值，以及相似或相關程度的詳細資訊。  
  
 [管理及監視語意搜尋](manage-and-monitor-semantic-search.md)  
 描述語意索引的程序以及與監視及管理索引相關的工作。  
  
##  <a name="relcontent"></a> 相關內容  
 [語意搜尋 DDL、函數、預存程序及檢視](../views/views.md)  
 列出加入或變更以支援統計語意搜尋的 Transact-SQL 陳述式和 SQL Server 資料庫物件。  
  
  
