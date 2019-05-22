---
title: sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db_TSQL
- sp_fulltext_semantic_unregister_language_statistics_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db
ms.assetid: 1426ca4a-9a76-489e-98da-8f6d13ff9732
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6aca3cf59d386dc9913103d69d00dc3ecb973283
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65982989"
---
# <a name="spfulltextsemanticunregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_unregister_language_statistics_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中取消註冊現有的語義語言統計資料庫，並且刪除任何相關聯的中繼資料。  
  
 這個陳述式不會卸離資料庫或從檔案系統移除實體資料庫檔案。 在取消註冊資料庫之後，您可以卸離資料庫並且刪除實體資料庫檔案。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
##  <a name="Arguments"></a> 引數  
 這個程序不需要任何引數。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體只有一個語義語言統計資料庫，所以不需要識別資料庫。  
  
## <a name="return-code-value"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-set"></a>結果集  
 無。  
  
## <a name="general-remarks"></a>一般備註  
 取消註冊語義語言統計資料庫時，同時也會移除所有相關聯的中繼資料。  
  
 **sp_fulltext_semantic_unregister_language_statistics_db**會執行下列步驟：  
  
1.  檢查目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體沒有語意母體擴展正在進行中。  
  
2.  移除與指定之語義語言統計資料庫相關聯的所有中繼資料。  
  
 如需詳細資訊，請參閱 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>中繼資料  
 執行個體上安裝之語義語言統計資料庫相關的資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，查詢目錄檢視[sys.fulltext_semantic_language_statistics_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何取消註冊語義語言統計資料庫，藉由呼叫**sp_fulltext_semantic_unregister_language_statistics_db**。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
