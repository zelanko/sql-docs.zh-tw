---
title: sys.dm_clr_appdomains (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7e1c3534e510e2a18929331918db7b6cf3efa60
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657457"
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對伺服器中每一個應用程式定義域，各傳回一個資料列。 應用程式定義域 (**AppDomain**) 是在建構[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) 是應用程式隔離的單位。 您可以使用此檢視來了解及疑難排解在中執行的 CLR 整合物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 CLR 整合 Managed 資料庫物件有多種類型。 如需這些物件的一般資訊，請參閱[利用 Common Language Runtime (CLR) 整合建置資料庫物件](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)。 執行這些物件時，每當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會建立**AppDomain**供其來載入及執行必要的程式碼。 隔離等級**AppDomain**是其中一個**AppDomain**每個資料庫每個擁有者。 也就是使用者所擁有的所有 CLR 物件一律會都執行在同一**AppDomain**每個資料庫 （如果使用者在不同資料庫中，CLR 資料庫物件將會執行不同的應用程式定義域中註冊 CLR 資料庫物件）。 **AppDomain**程式碼完成執行之後不會損毀。 而會將它快取到記憶體中，以供日後執行使用。 這可改善效能。  
  
 如需詳細資訊，請參閱 <<c0> [ 應用程式定義域](https://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|位址**AppDomain**。 所有受管理的資料庫使用者所擁有的物件永遠都會載入相同**AppDomain**。 您可以使用此資料行來查閱所有目前在此載入的組件**AppDomain**中**sys.dm_clr_loaded_assemblies**。|  
|**appdomain_id**|**int**|識別碼**AppDomain**。 每個**AppDomain**都有唯一的識別碼。|  
|**appdomain_name**|**varchar(386)**|名稱**AppDomain**所指派[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**creation_time**|**datetime**|時間**AppDomain**所建立。 因為**Appdomain**會快取並重複使用的較佳的效能**creation_time**不一定是程式碼執行時的時間。|  
|**db_id**|**int**|這個資料庫的識別碼**AppDomain**所建立。 儲存在兩個不同資料庫中的程式碼無法共用一個**AppDomain**。|  
|**user_id**|**int**|物件可以在此執行的使用者識別碼**AppDomain**。|  
|**state**|**nvarchar(128)**|目前狀態的描述元**AppDomain**。 任一 AppDomain 在從建立到刪除的期間，都可以有不同的狀態。 請參閱本主題的＜備註＞一節，以取得詳細資訊。|  
|**strong_refcount**|**int**|強式參考數目**AppDomain**。 這會反映目前正在執行使用此選項的批次的數字**AppDomain**。 請注意，執行此檢視將會建立**強式 refcount**; 即使目前正在執行，沒有程式碼**strong_refcount**會有值為 1。|  
|**weak_refcount**|**int**|弱式參考數目**AppDomain**。 這表示內的物件數目**AppDomain**會快取。 當您執行 managed 的資料庫物件，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]快取內**AppDomain**供日後重複使用。 這可改善效能。|  
|**cost**|**int**|成本**AppDomain**。 成本愈高，愈這**AppDomain**是記憶體不足的壓力而卸載。 通常，費用會取決於多少記憶體才能重新建立這**AppDomain**。|  
|**value**|**int**|值**AppDomain**。 值越小，比較這**AppDomain**是記憶體不足的壓力而卸載。 值通常取決於幾個連接或批次正在使用此**AppDomain**。|  
|**total_processor_time_ms**|**bigint**|自處理序啟動以來，在目前應用程式定義域中執行之所有執行緒所用的處理器總時間 (以毫秒為單位)。 這相當於**System.AppDomain.MonitoringTotalProcessorTime**。|  
|**total_allocated_memory_kb**|**bigint**|自應用程式定義域建立以來，它所進行的所有記憶體配置總大小 (以 KB 為單位)，不減去已回收的記憶體。 這相當於**System.AppDomain.MonitoringTotalAllocatedMemorySize**。|  
|**survived_memory_kb**|**bigint**|在上次完整區塊回收中存活下來且已知為目前應用程式定義域所參考的 KB 數。 這相當於**System.AppDomain.MonitoringSurvivedMemorySize**。|  
  
## <a name="remarks"></a>備註  
 一對多關聯性之間**dm_clr_appdomains.appdomain_address**並**dm_clr_loaded_assemblies.appdomain_address**。  
  
 下表列出可能**狀態**的值，其描述與發生在**AppDomain**生命週期。 您可以使用這項資訊来遵循的生命週期**AppDomain** ，以及監看可疑或重複**AppDomain**卸載，而不需剖析 Windows 事件記錄檔的執行個體。  
  
## <a name="appdomain-initialization"></a>AppDomain 初始化  
  
|State|描述|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|**AppDomain**正在建立。|  
  
## <a name="appdomain-usage"></a>AppDomain 使用方式  
  
|State|描述|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|執行階段**AppDomain**可供多個使用者使用。|  
|E_APPDOMAIN_SINGLEUSER|**AppDomain**可供 DDL 作業中使用。 這些與 E_APPDOMAIN_SHARED 不同，因為共用的 AppDomains 是用於 CLR 整合執行，與 DDL 作業相反。 這類的 AppDomains 會與其他的並行作業隔離。|  
|E_APPDOMAIN_DOOMED|**AppDomain**排定卸載時程，但目前沒有正在執行的執行緒。|  
  
## <a name="appdomain-cleanup"></a>AppDomain 清除  
  
|State|描述|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已要求 CLR 卸載**AppDomain**，通常是因為包含 managed 的資料庫物件的組件已改變或卸除。|  
|E_APPDOMAIN_UNLOADED|CLR 已卸載**AppDomain**。 這通常是因為升級程序的結果**threadabort byl Proces**， **OutOfMemory**，或在使用者程式碼中處理的例外狀況。|  
|E_APPDOMAIN_ENQUEUE_DESTROY|**AppDomain**已在 CLR 中卸載並設定為由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|E_APPDOMAIN_DESTROY|**AppDomain**過程中的終結[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|E_APPDOMAIN_ZOMBIE|**AppDomain**已終結[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 不過，並非所有參考**AppDomain**已清除。|  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何檢視的詳細資料**AppDomain**指定組件：  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 下列範例顯示如何檢視中的所有組件給定**AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_clr_loaded_assemblies &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [通用語言執行平台相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
