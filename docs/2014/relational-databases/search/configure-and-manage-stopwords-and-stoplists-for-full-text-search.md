---
title: 設定及管理全文檢索搜尋的停用字詞與停用字詞表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 103b5024368c5ca239856580e9b45473aabf6a92
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997650"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>設定及管理全文檢索搜尋的停用字詞與停用字詞表
  為精簡全文檢索索引， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有一種機制，可捨棄無助於搜尋卻經常出現的字串。 這些捨棄的字串稱為 *「停用字詞」* (Stopword)。 在索引建立期間，全文檢索引擎會從全文檢索索引省略停用字詞。 這代表全文檢索查詢不會搜尋停用字詞。  
  
##  <a name="understanding-stopwords-and-stoplists"></a><a name="understand"></a>瞭解停用字詞和字詞  
 停用字詞表可以是具有特定語言意義的字詞，或者也可以是不具有語言意義的 *token* 。 例如，在英文中，"a"、"and"、"is" 及 "the" 等字會排除在全文檢索索引外，因為一般而言這些字都無助於搜尋。  
  
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
  
 資料庫中的停用字詞是使用稱為停用字詞表的物件來管理。 停用*字*詞表是停用字詞的清單，與全文檢索索引相關聯時，會套用至該索引上的全文檢索查詢。  
  
  
##  <a name="creating-a-stoplist"></a><a name="creating"></a>建立停用字詞表  
 您可以使用下列任一方式建立停用字詞表：  
  
-   在資料庫中使用系統提供的停用字詞表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隨附一份系統停用字詞表，其中包含每種受支援語言的常用停用字詞，而且適用於預設與給定斷詞工具相關聯的每種語言。 此系統停用字詞表包含所有受支援語言的常見停用字詞。  您可以複製此系統停用字詞表，並且透過加入和移除停用字詞，自訂您的複本。  
  
     系統停用字詞表是安裝在 [資源](../databases/resource-database.md) 資料庫。  
  
-   建立自己的停用字詞表，然後針對您指定的任何語言，在此停用字詞表中加入停用字詞。 您也可以在必要時從停用字詞表卸除停用字詞。  
  
-   在目前的伺服器執行個體中使用來自任何其他資料庫的現有自訂停用字詞表，然後再視需要加入和卸除停用字詞。  
  
 **若要建立停用字詞表**  
  
-   [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)  
  
#### <a name="to-create-a-full-text-stoplist-in-management-studio"></a>在 Management Studio 中建立全文檢索停用字詞表  
  
1.  在 [物件總管] 中，展開伺服器。  
  
2.  展開 [資料庫]****，然後展開含有您要建立全文檢索停用字詞表的資料庫。  
  
3.  展開 [儲存體]****，然後以滑鼠右鍵按一下 [全文檢索停用字詞表]****。  
  
4.  選取 [新增全文檢索停用字詞表]****。  
  
5.  指定停用字詞表名稱。  
  
6.  選擇將某個其他人指定為停用字詞表的擁有者。  
  
7.  選取下列建立停用字詞表選項的其中一個：  
  
    -   **建立空的停用字詞表**  
  
    -   **從系統停用字詞表建立**  
  
    -   **從現有全文檢索停用字詞表建立**  
  
     如需詳細資訊，請參閱[新增全文檢索停用字詞表 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **卸除停用字詞表**  
  
-   [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
##  <a name="using-a-stoplist-in-full-text-queries"></a><a name="queries"></a>在全文檢索查詢中使用停用字詞表  
 若要在查詢中使用停用字詞表，您必須將其與全文檢索索引產生關聯。 您可以在建立索引時將停用字詞表附加到全文檢索索引，也可以之後再更改索引以加入停用字詞表。  
  
 **建立全文檢索索引並讓停用字詞表與其產生關聯**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **讓停用字詞表與現有的全文檢索索引產生關聯或取消關聯**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **如果停用字詞造成全文檢索查詢的布林運算失敗，則抑制錯誤訊息的顯示**  
  
-   [轉換非搜尋字伺服器組態選項](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)  
  
  
##  <a name="viewing-stoplists-and-stoplist-metadata"></a><a name="viewing"></a>查看字詞和停用字詞表中繼資料  
 **檢視停用字詞表的所有停用字詞**  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
 **取得有關目前資料庫中所有停用字詞表的詳細資訊**  
  
-   [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
 **檢視斷詞工具、同義字及停用字詞表組合的 Token 化結果**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
  
##  <a name="changing-the-stopwords-in-a-stoplist"></a><a name="change"></a>變更停用字詞表中的停用字詞  
 **在停用字詞表中加入或卸除停用字詞**  
  
-   [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)  
  
#### <a name="to-change-the-stopwords-in-a-stoplist-in-management-studio"></a>在 Management Studio 中變更停用字詞表中的停用字詞  
  
1.  在 [物件總管] 中，展開伺服器。  
  
2.  展開 **[資料庫]**，然後展開此資料庫。  
  
3.  展開 **[儲存體]**，然後選取 **[全文檢索停用字詞表]**。  
  
4.  以滑鼠右鍵按一下要變更屬性的停用字詞表，然後選取 [屬性]****。  
  
5.  在 [[全文檢索停用字詞表屬性]](../../database-engine/full-text-stoplist-properties.md) 對話方塊中：  
  
    1.  在 **[動作]** 清單方塊中，選取下列其中一個動作： **[加入停用字詞]**、 **[刪除停用字詞]**、 **[刪除所有停用字詞]** 或 **[清除停用字詞表]**。  
  
    2.  如果已針對選定動作啟用 **[停用字詞]** 文字方塊，請輸入單一停用字詞。 這個停用字詞必須是唯一的，亦即，尚未存在您所選取之語言的這個停用字詞表中。  
  
    3.  如果已針對選定動作啟用 [全文檢索語言]**** 清單方塊，請選取語言。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
##  <a name="upgrading-noise-words-from-sql-server-2005"></a><a name="upgrade"></a>從 SQL Server 2005 升級非搜尋字  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 非搜尋字已經由停用字詞所取代。 當資料庫從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]升級時，便不再使用非搜尋字檔案。 不過，這些非搜尋字檔案會儲存在 FTDATA\ FTNoiseThesaurusBak 資料夾中，而且您之後可以在更新或建立對應的停用字詞表時使用它們。 如需如何將非搜尋字檔案升級為停用字詞表的資訊，請參閱 [升級全文檢索搜尋](upgrade-full-text-search.md)。  
  
  
  
