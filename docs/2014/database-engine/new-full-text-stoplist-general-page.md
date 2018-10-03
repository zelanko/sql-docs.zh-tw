---
title: 新全文檢索停用字詞表 （一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplist.general.f1
ms.assetid: 97f8e82d-82ab-4525-91c9-1ee3ae217309
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: eca5e82b9d23709b45949cfe6af9022f1243ef08
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066348"
---
# <a name="new-full-text-stoplist-general-page"></a>新增全文檢索停用字詞表 (一般頁面)
  使用這個對話方塊，即可建立全文檢索停用字詞表。 *「停用字詞表」* (Stoplist) 是指一組稱為 *「停用字詞」*(Stopword) 的常用字，而使用該停用字詞表之資料表的全文檢索索引會省略這些字。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/full-text-search.md)。  
  
 **若要使用 SQL Server Management Studio 來建立停用字詞表**  
  
-   [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>選項。  
 **全文檢索停用字詞表名稱**  
 輸入全文檢索停用字詞表的名稱。  
  
 **[擁有者]**  
 指定全文檢索停用字詞表的擁有者。 如果您想要將擁有權指派給自己 (亦即，目前的使用者)，請將這個欄位保留空白。  
  
 若要指定不同的使用者，請按一下瀏覽按鈕。  
  
### <a name="create-stoplist-options"></a>建立停用字詞表選項  
 按一下下列其中一個建立選項：  
  
 **建立空的停用字詞表**  
 新的停用字詞表將不會包含任何停用字詞。  
  
 **從系統停用字詞表建立**  
 新的停用字詞表是從預設存在於 [Resource 資料庫](../relational-databases/databases/resource-database.md)中的停用字詞表所建立。  
  
 **從現有全文檢索停用字詞表建立**  
 新的停用字詞表是藉由複製現有的停用字詞表所建立。  
  
 **來源資料庫**  
 指定現有停用字詞表所屬的資料庫名稱。 系統預設會選取目前的資料庫。 (選擇性) 請從清單方塊中選取不同的資料庫。  
  
 **來源停用字詞表**  
 指定現有停用字詞表的名稱。 從可用停用字詞表的清單中，選取要當做來源使用的停用字詞表。 可用的停用字詞表會按照它們顯示在 [物件總管] 中的順序列出。  
  
 如果來源停用字詞表中停用字詞內指定的任何語言未在目前資料庫中註冊，則 CREATE FULLTEXT STOPLIST 會成功，但是會傳回警告，而且不會加入對應的停用字詞。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)   
 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
  
