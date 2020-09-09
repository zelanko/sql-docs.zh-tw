---
description: sp_fulltext_service (Transact-SQL)
title: sp_fulltext_service (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_service
- sp_fulltext_service_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- sp_fulltext_service
- Full-Text Search Upgrade Option
ms.assetid: 17a91433-f9b6-4a40-88c4-8c704ec2de9f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f29ad11ca5b1df94e445466a5402637a2abab023
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546118"
---
# <a name="sp_fulltext_service-transact-sql"></a>sp_fulltext_service (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索搜尋的伺服器屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_fulltext_service [ [@action=] 'action'   
     [ , [ @value= ] value ] ]  
```  
  
## <a name="arguments"></a>引數  
`[ @action = ] 'action'` 這是要變更或重設的屬性。 *動作* 是 **Nvarchar (100) ，** 沒有預設值。 如需*c*使用者屬性的清單、其描述，以及可設定的值，請參閱 *value* 引數底下的表格。 這個引數會傳回下列屬性：資料類型、目前執行中的值、最小值或最大值，以及已被取代的狀態 (如果適用的話)。  
  
`[ @value = ] value` 這是指定之屬性的值。 *值* 是 **SQL_variant**，預設值是 Null。 如果 @value 是 null， **sp_fulltext_service** 會傳回目前的設定。 這份資料表會列出動作屬性及其描述，以及可設定的值之清單。  
  
> [!NOTE]  
>  下列動作將在未來的版本中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ： **clean_up**、 **connect_timeout**、 **data_timeout**和 **resource_usage**。 請避免在新的開發工作中使用這些動作，並規劃修改目前使用任何這些動作的應用程式。  
  
|動作|資料類型|描述|  
|------------|---------------|-----------------|  
|**clean_up**|**int**|支援這個項目的目的，只是為了與舊版相容。 這個值一定是 0。|  
|**connect_timeout**|**int**|支援這個項目的目的，只是為了與舊版相容。 這個值一定是 0。|  
|**data_timeout**|**int**|支援這個項目的目的，只是為了與舊版相容。 這個值一定是 0。|  
|**load_os_resources**|**int**|指出是否註冊了作業系統斷詞工具、字幹分析器和篩選，以及是否搭配這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來使用它們。 值為下列其中之一：<br /><br /> 0 = 只用這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體專用的篩選和斷詞工具。<br /><br /> 1 = 載入作業系統篩選和斷詞工具。<br /><br /> 根據預設，系統會停用這個屬性來防止因更新作業系統而意外變更行為。 啟用作業系統資源會提供已向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 索引服務註冊，但並未安裝特定執行個體專用資源之語言和文件類型資源的存取權。 如果您啟用作業系統資源的載入，請確定作業系統資源是受信任的已簽署二進位檔;否則，當 **verify_signature** 時，無法載入它們 (請參閱以下) 設定為1。|  
|**master_merge_dop**|**int**|指定主要合併程序所要使用的執行緒數目。 此值不應超過可用 CPU 或 CPU 核心的數量。<br /><br /> 如果未指定這個引數，服務會使用 4 或是可用 CPU 或 CPU 核心數量 (取兩者中較小的那一個)。|  
|**pause_indexing**|**int**|指定全文檢索索引是應該暫停 (如果它目前正在執行) 還是繼續 (如果它目前已暫停)。<br /><br /> 0 = 繼續伺服器執行個體的全文檢索索引活動。<br /><br /> 1 = 暫停伺服器執行個體的全文檢索索引活動。|  
|**resource_usage**|**int**|在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中沒有作用，所以會予以忽略。|  
|**update_languages**|NULL|更新使用全文檢索搜尋所註冊的語言和篩選清單。 這些語言是在設定索引和進行全文檢索查詢時所指定。 篩選背景程式主機會使用篩選器，從對應的檔案格式（例如，在資料類型中儲存的 .docx，例如 **Varbinary**、 **Varbinary (max) **、 **image**或 **xml**）解壓縮文字資訊，以進行全文檢索索引。<br /><br /> 如需詳細資訊，請參閱 [檢視或變更已註冊的篩選與斷詞工具](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)。|  
|**upgrade_option**|**int**|控制將資料庫從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升級到更新版本時，要如何移轉全文檢索索引。 這個屬性適用於以下方式的升級：附加資料庫、還原資料庫備份、還原檔案備份，或是使用複製資料庫精靈複製資料庫。<br /><br /> 值為下列其中之一：<br /><br /> 0 = 全文檢索目錄會使用新的增強斷詞工具重建。 重建索引可能要花一些時間，而且在升級之後可能需要相當多的 CPU 和記憶體。<br /><br /> 1 = 重設全文檢索目錄。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 全文檢索目錄檔案會遭到移除，但是全文檢索目錄和全文檢索索引的中繼資料則會保留。 在升級之後，所有的全文檢索索引都會停用變更追蹤，而且不會自動啟動搜耙。 當您在升級完成之後手動發出完整母體擴展之前，此目錄將會維持空白狀態。<br /><br /> 2 = 匯入全文檢索目錄。 一般而言，匯入的速度明顯比重建的速度更快。 例如，只有使用一個 CPU 時，匯入的執行速度大約比重建的速度快 10 倍。 不過，匯入的全文檢索目錄並不會使用新增的強化斷詞工具，所以您最後可能會想要重建全文檢索目錄。<br /><br /> 注意：重建可以在多執行緒模式中執行，如果有10個以上的 Cpu 可用，如果您允許重建以使用所有 Cpu，重建的執行速度可能會比匯入更快。<br /><br /> 如果無法使用全文檢索目錄，將會重建關聯的全文檢索索引。 只有針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫才可以使用此選項。<br /><br /> 如需選擇全文檢索升級選項的資訊，請參閱[升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。<br /><br /> 注意：若要在中設定此屬性 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，請使用 **全文檢索升級選項** 屬性。 如需詳細資訊，請參閱 [管理及監視伺服器執行個體的全文檢索搜尋](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)。|  
|**verify_signature**|**int**|指出全文檢索引擎是否只載入已簽署的二進位檔。 依預設，只會載入受信任的已簽署之二進位檔。<br /><br /> 1 = 確認只載入受信任的已簽署之二進位檔 (預設值)。<br /><br /> 0 = 不驗證是否已簽署二進位檔。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>權限  
 只有 **serveradmin** 固定伺服器角色的成員或系統管理員可以執行 **sp_fulltext_service**。  
  
## <a name="examples"></a>範例  
  
### <a name="a-updating-the-list-of-registered-languages"></a>A. 更新已註冊的語言清單  
 下列範例會更新已向全文檢索搜尋註冊的語言清單。  
  
```  
EXEC sp_fulltext_service 'update_languages';  
GO  
```  
  
### <a name="b-changing-the-full-text-upgrade-option-to-reset-full-text-catalogs"></a>B. 變更全文檢索升級選項來重設全文檢索目錄  
 下列範例會變更全文檢索升級選項來重設全文檢索目錄， 這樣會將它們完全移除。 此範例會指定選擇性 `@action` 和 `@value` 關鍵字。  
  
```  
EXEC sp_fulltext_service @action='upgrade_option', @value=1;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
