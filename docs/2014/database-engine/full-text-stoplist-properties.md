---
title: 全文檢索停用字詞表屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4cfdd308ab7488633721ddaac55d3d926a276b0d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779405"
---
# <a name="full-text-stoplist-properties"></a>全文檢索停用字詞表屬性
  使用此對話方塊可加入或刪除個別停用字詞、刪除特定語言的所有停用字詞，或是清除目前的停用字詞表。 停用字詞是停用字詞表內所包含的常用字。 使用某停用字詞表之資料表的全文檢索索引中會省略該停用字詞表內的停用字詞。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/full-text-search.md)。  
  
 **使用 SQL Server Management Studio 變更停用字詞表屬性**  
  
-   [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>選項。  
 **動作**  
 指定您要執行的動作。  
  
 **加入停用字詞**  
 將常用字加入停用字詞表。  
  
 **刪除停用字詞**  
 從停用字詞表中刪除停用字詞。  
  
 **刪除所有停用字詞**  
 刪除特定語言的所有停用字詞。  
  
 **清除停用字詞表**  
 刪除所有語言的所有停用字詞來清除停用字詞表。  
  
 **停用字詞**  
 如果您已選取 **[加入停用字詞]** 或 **[刪除停用字詞]**，請在 **[停用字詞]** 欄位中輸入停用字詞。 新的停用字詞必須是唯一的，亦即，尚未存在您所選取之語言的這個停用字詞表中。  
  
 **全文檢索語言**  
 如果您已選取 **[加入停用字詞]**、 **[刪除停用字詞]** 或 **[刪除所有停用字詞]**，請從清單方塊中選取停用字詞的語言。 這樣會列出伺服器執行個體支援的所有全文檢索語言。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/full-text-search.md)   
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
