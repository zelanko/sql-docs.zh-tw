---
title: "sys.fulltext_languages (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb66c10f797c7951f54125c7b5b99cfc25f983ee
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysfulltextlanguages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  這份目錄檢視會針對其斷詞工具向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊的每種語言，各包含一個資料列。 每個資料列顯示的 LCID 和語言的名稱。 針對某種語言註冊斷詞工具時，其他語言資源 (字幹分析器、非搜尋字 (停用字詞) 和同義字檔案) 就會成為可供全文檢索索引/查詢作業使用。 值**名稱**或**lcid**全文檢索索引與全文檢索查詢中可以指定[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。  
   
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|**lcid**|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 地區設定識別碼 (LCID) 的語言。|  
|**name**|**sysname**|是中的別名值[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)的值對應**lcid**或是數值 LCID 的字串表示。|  
  
## <a name="values-returned-for-default-languages"></a>針對預設語言傳回的值  
 下表顯示預設註冊其斷詞工具之語言的值。  
  
|語言|LCID|  
|--------------|----------|  
|阿拉伯文|1025|  
|孟加拉文 (印度)|1093|  
|英式英文|2057|  
|保加利亞文|1026|  
|卡達隆尼亞文|1027|  
|中文 (香港特別行政區、中國)|3076|  
|中文 (澳門特別行政區)|5124|  
|中文 (新加坡)|4100|  
|克羅埃西亞文|1050|  
|捷克文|1029|  
|丹麥文|1030|  
|荷蘭文|1043|  
|英文|1033|  
|法文|1036|  
|德文|1031|  
|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 希臘文|1032|  
|古吉拉特文|1095|  
|Hebrew|1037|  
|Hindi|1081|  
|冰島文|1039|  
|印尼文|1057|  
|義大利文|1040|  
|日文|1041|  
|坎那達文|1099|  
|韓文|1042|  
|拉脫維亞文|1062|  
|立陶宛文|1063|  
|馬來文 - 馬來西亞|1086|  
|馬來亞拉姆文|1100|  
|馬拉提文|1102|  
|中性語言|0|  
|挪威文 (巴克摩)|1044|  
|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 波蘭文|1045|  
|葡萄牙文 (巴西)|1046|  
|葡萄牙文 (葡萄牙)|2070|  
|旁遮普文|1094|  
|羅馬尼亞文|1048|  
|俄文|1049|  
|塞爾維亞文 (斯拉夫)|3098|  
|塞爾維亞文 (拉丁)|2074|  
|簡體中文|2052|  
|斯洛伐克文|1051|  
|斯洛維尼亞文|1060|  
|西班牙文|3082|  
|瑞典文|1053|  
|坦米爾文|1097|  
|特拉古文|1098|  
|泰文|1054|  
|繁體中文|1028|  
|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 土耳其文|1055|  
|烏克蘭文|1058|  
|烏都文|1056|  
|越南文|1066|  
  
## <a name="remarks"></a>備註  
 若要更新使用全文檢索搜尋註冊之語言清單，請使用[sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**'。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [設定及管理全文檢索搜尋停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
