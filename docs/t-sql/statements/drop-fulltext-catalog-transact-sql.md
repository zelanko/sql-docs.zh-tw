---
title: "DROP FULLTEXT CATALOG (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_CATALOG_TSQL
- DROP FULLTEXT CATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- dropping full-text catalogs
- removing full-text catalogs
- full-text catalogs [SQL Server], removing
- deleting full-text catalogs
- DROP FULLTEXT CATALOG statement
ms.assetid: b54efb0b-400b-49ce-923b-ce20a2a12255
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32445ba8410673168ffe8e7da61cdd1b37d71afe
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-fulltext-catalog-transact-sql"></a>DROP FULLTEXT CATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從資料庫中移除全文檢索目錄。 在卸除目錄之前，您必須先卸除與目錄相關的所有全文檢索索引。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP FULLTEXT CATALOG catalog_name  
```  
  
## <a name="arguments"></a>引數  
 *catalog_name*  
 這是要移除的目錄名稱。 如果*catalog_name*不存在， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會傳回錯誤並不會執行 DROP 作業。 全文檢索目錄的檔案群組不能標示 OFFLINE 或 READONLY，命令才能順利完成。  
  
## <a name="permissions"></a>Permissions  
 使用者必須有全文檢索目錄的 DROP 權，或必須屬於**db_owner**，或**db_ddladmin**固定資料庫角色。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fulltext_catalogs &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [建立全文檢索目錄 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  

