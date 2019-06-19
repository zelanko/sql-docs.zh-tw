---
title: 搜尋屬性清單編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.searchpropertylisteditor.f1
ms.assetid: 0f3ced6e-0dfd-49fc-b175-82378c3d668e
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 818e1176cb5a4f81205a36dc7be6fd9fded286ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773666"
---
# <a name="search-property-list-editor"></a>搜尋屬性清單編輯器
  使用此對話方塊來新增或刪除搜尋屬性清單中的搜尋屬性。  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>若要使用 SQL Server Management Studio 管理搜尋屬性清單  
 如需有關如何建立、 檢視或刪除搜尋屬性清單，以及如何設定屬性搜尋的全文檢索索引資訊，請參閱 < [Search Document Properties with Search Property Lists](../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="options"></a>選項  
 **屬性名稱**  
 指定要用來識別全文檢索查詢中之屬性的名稱。 屬性名稱可以包含內部空格。 **[屬性名稱]** 的最大長度為 256 個字元。 這個名稱可以是使用者易記名稱，例如「作者」或「住家地址」，或者它可以是屬性的 Windows 正式名稱，例如 `System.Author` 或 `System.Contact.HomeAddress`。 **[屬性名稱]** 必須唯一識別屬性集內的屬性。  
  
 開發人員使用屬性名稱來識別 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 述詞中的屬性。 因此，在加入屬性時，務必指定可有意義地表示屬性的值。  
  
 **屬性集 GUID**  
 指定屬性所屬之屬性集的識別碼。 這是全域唯一識別碼 (GUID)。 屬性集是一組邏輯相關的屬性。 如需有關取得此值的詳細資訊，請參閱本主題稍後的＜備註＞。  
  
 **屬性 Int 識別碼**  
 指定屬性的屬性整數識別碼。 這個預先指派的值是屬性集內唯一的正整數。 如需有關取得此值的詳細資訊，請參閱本主題稍後的＜備註＞。  
  
> [!NOTE]  
>  全文檢索搜尋不支援使用字串識別碼的文件屬性。  
  
 **屬性描述**  
 選擇性地指定屬性的描述。 這是最多 512 個字元的字串。 例如，描述可能包含有關屬性所屬之屬性集的詳細資訊，或有關與其名稱不盡相符之屬性的詳細資訊。  
  
## <a name="remarks"></a>備註  
 若要將搜尋屬性加入至搜尋屬性清單，您必須指定屬性所屬之屬性集的全域唯一識別碼 (GUID)，以及屬性的屬性整數識別碼。 兩者的指定組合在給定的搜尋屬性清單中必須是唯一的。 如果您嘗試加入現有的組合，作業就會失敗並發出錯誤。 這表示您只能設定給定屬性的一個名稱。  
  
 屬性描述是選擇性的。  
  
 **若要設定全文檢索索引的搜尋屬性清單**  
  
-   [使用搜索屬性清單搜索文件屬性](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
## <a name="permissions"></a>Permissions  
 請參閱[ALTER SEARCH PROPERTY LIST &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)   
 [使用搜索屬性清單搜索文件屬性](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
