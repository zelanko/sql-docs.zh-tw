---
title: 新增搜尋屬性清單 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.newsearchpropertylist.f1
ms.assetid: ffca78e9-8608-4b15-bd38-b2d78da4247a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2aff15a42c8bffeb5a54e92b9ce7a09ace282ce4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774496"
---
# <a name="new-search-property-list"></a>新增搜尋屬性清單
  使用這個對話方塊來建立搜尋屬性清單。  
  
## <a name="options"></a>選項。  
 **搜尋屬性清單名稱**  
 請輸入搜尋屬性清單的名稱。  
  
 **擁有者**  
 指定搜尋屬性清單的擁有者。 如果您想要將擁有權指派給自己 (亦即，目前的使用者)，請將這個欄位保留空白。 若要指定不同的使用者，請按一下瀏覽按鈕。  
  
### <a name="create-search-property-list-options"></a>建立搜尋屬性清單選項  
 請按一下下列其中一個選項：  
  
 **建立空的搜尋屬性清單**  
 建立沒有任何屬性的搜尋屬性清單。  
  
 **從現有搜尋屬性清單建立**  
 將現有搜尋屬性清單的屬性複製到新的屬性清單中。 搜尋屬性清單是資料庫物件，所以您必須指定包含要複製之屬性清單的資料庫。  
  
 **源資料庫**  
 指定現有搜尋屬性清單所屬的資料庫名稱。 系統預設會選取目前的資料庫。 另外，如果目前連接與另一個資料庫中的使用者識別碼相關聯，您也可以選擇使用清單方塊來選取該資料庫。  
  
 **來源搜尋屬性清單**  
 從屬於選取之資料庫的搜尋屬性清單，選取現有的搜尋屬性清單名稱。  
  
## <a name="permissions"></a>權限  
 請參閱[&#40;transact-sql&#41;建立搜尋屬性清單](/sql/t-sql/statements/create-search-property-list-transact-sql)。  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>若要使用 SQL Server Management Studio 管理搜尋屬性清單  
 如需如何建立、檢視、變更或刪除搜尋屬性清單，以及如何設定全文檢索索引以進行屬性搜尋的詳細資訊，請參閱＜ [Search Document Properties with Search Property Lists](../relational-databases/search/search-document-properties-with-search-property-lists.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [建立搜尋屬性清單 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql)   
 [使用搜尋屬性清單搜尋文件屬性](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
