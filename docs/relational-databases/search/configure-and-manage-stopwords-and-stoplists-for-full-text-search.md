---
title: 設定及管理全文檢索搜尋的停用字詞與停用字詞表 | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], noise words
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e7f87bdfcbebe8843564a95a9f38f5d69a649cd1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729636"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>設定及管理全文檢索搜尋的停用字詞與停用字詞表
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  為精簡全文檢索索引， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有一種機制，可捨棄無助於搜尋卻經常出現的字串。 這些捨棄的字串稱為 *「停用字詞」*(Stopword)。 在索引建立期間，全文檢索引擎會從全文檢索索引省略停用字詞。 這代表全文檢索查詢不會搜尋停用字詞。  
   
**停用字詞**。 停用字詞可能是具有特定語言意義的字詞。 例如，在英文中，"a"、"and"、"is" 及 "the" 等字會排除在全文檢索索引外，因為一般而言這些字都無助於搜尋。 停用字詞也可能是不具有語言意義的 *Token*。  

**停用字詞表**。 資料庫中的停用字詞是使用稱為停用字詞表的物件來管理。 「停用字詞表」是停用字詞的清單，與全文檢索索引相關聯時，會套用至該索引上的全文檢索查詢。
   
## <a name="use-an-existing-stoplist"></a>使用現有的停用字詞表  
 您可以透過下列方式使用現有的停用字詞表：  
  
-   在資料庫中使用系統提供的停用字詞表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隨附一份系統停用字詞表，其中包含每種支援語言的常用停用字詞，而且適用於預設與特定斷詞工具相關聯的每種語言。 您可以複製這份系統停用字詞表，並透過新增和移除停用字詞來自訂您的複本。  
  
     系統停用字詞表是安裝在 [資源](../../relational-databases/databases/resource-database.md) 資料庫。  
  
-   在目前的伺服器執行個體中，使用來自其他資料庫的現有自訂停用字詞表，然後適當新增和卸除停用字詞。  
  
## <a name="create-a-new-stoplist"></a>建立新的停用字詞表 
### <a name="create-a-new-stoplist-with-transact-sql"></a>使用 Transact-SQL 建立新的停用字詞表
使用 [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)。

### <a name="create-a-new-stoplist-with-management-studio"></a>使用 Management Studio 建立新的停用字詞表
  
1.  在 [物件總管] 中，展開伺服器。  
  
2.  展開 [資料庫]，然後展開含有您要建立全文檢索停用字詞表的資料庫。  
  
3.  展開 [儲存體]，然後以滑鼠右鍵按一下 [全文檢索停用字詞表]。  
  
4.  選取 [新增全文檢索停用字詞表]。  
  
5.  輸入新的停用字詞表名稱。  
  
6.  選擇將某個其他人指定為停用字詞表的擁有者。  
  
7.  選取下列建立停用字詞表選項的其中一個：  
  
    -   **建立空的停用字詞表**  
  
    -   **從系統停用字詞表建立**  
  
    -   **從現有全文檢索停用字詞表建立**  
  
     如需詳細資訊，請參閱[新增全文檢索停用字詞表 &#40;一般頁面&#41;](http://msdn.microsoft.com/library/97f8e82d-82ab-4525-91c9-1ee3ae217309)。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="use-a-stoplist-in-full-text-queries"></a>在全文檢索查詢中使用停用字詞表  
 若要在查詢中使用停用字詞表，您必須將其與全文檢索索引產生關聯。 您可以在建立索引時將停用字詞表附加到全文檢索索引，也可以之後再更改索引以加入停用字詞表。  
  
### <a name="create-a-full-text-index-and-associate-a-stoplist-with-it"></a>建立全文檢索索引並將停用字詞表與其產生關聯
使用 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)。
  
### <a name="associate-or-disassociate-a-stoplist-with-an-existing-full-text-index"></a>將停用字詞表與現有的全文檢索索引產生關聯或取消關聯
使用 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)。 
  
## <a name="change-the-stopwords-in-a-stoplist"></a>變更停用字詞表中的停用字詞  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-transact-sql"></a>使用 Transact-SQL，在停用字詞表中新增或卸除停用字詞
使用 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)。
  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-management-studio"></a>使用 Management Studio，在停用字詞表中新增或卸除停用字詞  
  
1.  在 [物件總管] 中，展開伺服器。  
  
2.  展開 **[資料庫]**，然後展開此資料庫。  
  
3.  展開 **[儲存體]**，然後選取 **[全文檢索停用字詞表]**。  
  
4.  以滑鼠右鍵按一下要變更屬性的停用字詞表，然後選取 [屬性]。  
  
5.  在 [[全文檢索停用字詞表屬性]](http://msdn.microsoft.com/library/2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f) 對話方塊中：  
  
    1.  在 **[動作]** 清單方塊中，選取下列其中一個動作： **[加入停用字詞]**、 **[刪除停用字詞]**、 **[刪除所有停用字詞]** 或 **[清除停用字詞表]**。  
  
    2.  如果已針對選定動作啟用 **[停用字詞]** 文字方塊，請輸入單一停用字詞。 這個停用字詞必須是唯一的，亦即，尚未存在您所選取之語言的這個停用字詞表中。  
  
    3.  如果已針對選定動作啟用 [全文檢索語言] 清單方塊，請選取語言。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="manage-stoplists-and-their-usage"></a>管理停用字詞表和其使用方式
  
### <a name="view-all-the-stopwords-in-a-stoplist"></a>檢視停用字詞表中的所有停用字詞
使用 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)。 
  
### <a name="get-info-about-all-the-stoplists-in-the-current-database"></a>取得目前資料庫中所有停用字詞表的資訊
使用 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md) 和  [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)。
  
### <a name="view-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a>檢視斷詞工具、同義字及停用字詞表組合的 Token 化結果
使用 [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)。

### <a name="suppress-an-error-message-if-stopwords-cause-a-boolean-operation-on-a-full-text-query-to-fail"></a>如果停用字詞造成全文檢索查詢的布林運算失敗，則隱藏錯誤訊息
使用[轉換非搜尋字伺服器組態選項](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)。 
   
## <a name="more-info-about-stopword-position"></a>停用字詞位置的詳細資訊
 雖然全文檢索索引會略過包含的停用字詞，但仍會考慮其位置。 例如，請參考例句 "Instructions are applicable to these Adventure Works Cycles models"。 下表說明這些單字在片語中的位置：  
  
|Word|位置|  
|----------|--------------|  
|Instructions|1|  
|are|2|  
|applicable|3|  
|to|4|  
|these|5|  
|Adventure|6|  
|Works|7|  
|Cycles|8|  
|模型|9|  
  
 停用字詞 "are"、"to" 及 "these"，分別為第 2、第 4 及第 5 個字，這些文字都不會包含在全文檢索索引中。 但仍會保留這些文字的位置資訊，使句子中其他文字的位置不受影響。   
  
## <a name="upgrade-noise-words-from-sql-server-2005"></a>從 SQL Server 2005 升級非搜尋字  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 非搜尋字已經由停用字詞所取代。 當資料庫從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]升級時，便不再使用非搜尋字檔案。 不過，這些非搜尋字檔案會儲存在 FTDATA\ FTNoiseThesaurusBak 資料夾中，而且您之後可以在更新或建立對應的停用字詞表時使用它們。 如需如何將非搜尋字檔案升級為停用字詞表的資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
  
  
