---
title: sys.fulltext_semantic_languages & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: f1acc995223ba9785055839beb5e12b11ea7494f
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945666"
---
# <a name="sysfulltextsemanticlanguages-transact-sql"></a>sys.fulltext_semantic_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上註冊語義模型的每個語言，各傳回一個資料列。 當語言模型已註冊時，該語言會啟用語意索引。  
  
 這份目錄檢視是類似[sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。  
    
||||  
|-|-|-|  
|**資料行名稱**|**型別**|**說明**|  
|lcid|ssNoversion|語言的 Microsoft Windows 地區設定識別碼 (LCID)。|  
|NAME|sysname|不是值中的別名[sys.syslanguages &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)的值相對應**lcid**，或是數值 LCID 的字串表示法。|  
  
## <a name="general-remarks"></a>一般備註  
 如需詳細資訊，請參閱 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需有關支援語意索引已安裝語意語言統計資料庫的詳細資訊，請查詢目錄檢視[sys.fulltext_semantic_language_statistics_database &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。  
  
## <a name="examples"></a>範例  
 下列範例示範如何查詢**sys.fulltext_semantic_languages**若要取得所有語言模型已註冊的相關資訊的語意索引的目前執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
