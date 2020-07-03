---
title: sys.databases dm_clr_appdomains （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2c3c0351bd541738e2540cc1a0624cf0ca9836c5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893982"
---
# <a name="sysdm_clr_appdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對伺服器中每一個應用程式定義域，各傳回一個資料列。 應用程式域（**AppDomain**）是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 通用語言執行時間（CLR）中的結構，也就是應用程式的隔離單位。 您可以使用此視圖來瞭解和疑難排解在中執行的 CLR 整合物件 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 CLR 整合 Managed 資料庫物件有多種類型。 如需這些物件的一般資訊，請參閱[使用 Common Language Runtime （CLR）整合建立資料庫物件](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)。 每當執行這些物件時，會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立一個**AppDomain** ，供它用來載入及執行必要的程式碼。 **Appdomain**的隔離等級是每個擁有者每個資料庫的一個**AppDomain** 。 也就是說，使用者擁有的所有 CLR 物件一律會在每個資料庫的相同**AppDomain**中執行（如果使用者在不同的資料庫中註冊 clr 資料庫物件，CLR 資料庫物件將會在不同的應用程式域中執行）。 在程式碼完成執行之後， **AppDomain**不會終結。 而會將它快取到記憶體中，以供日後執行使用。 這樣可以提高執行效能。  
  
 如需詳細資訊，請參閱[應用程式域](https://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
|資料行名稱|資料類型|說明|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|**AppDomain**的位址。 使用者所擁有的所有 managed 資料庫物件一律會載入相同的**AppDomain**中。 您可以使用這個資料行，在 sys.databases 中查閱目前載入此**AppDomain**中的所有元件**dm_clr_loaded_assemblies**。|  
|**appdomain_id**|**int**|**AppDomain**的識別碼。 每個**AppDomain**都有唯一的識別碼。|  
|**appdomain_name**|**Varchar （386）**|所指派之**AppDomain**的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**creation_time**|**datetime**|**AppDomain**的建立時間。 因為已快取並重複使用**appdomain**來提升效能，所以**creation_time**不一定是執行程式碼的時間。|  
|**db_id**|**int**|建立此**AppDomain**所在的資料庫識別碼。 儲存在兩個不同資料庫中的程式碼無法共用一個**AppDomain**。|  
|**user_id**|**int**|其物件可在此**AppDomain**中執行之使用者的識別碼。|  
|**state**|**nvarchar(128)**|**AppDomain**目前狀態的描述項。 任一 AppDomain 在從建立到刪除的期間，都可以有不同的狀態。 請參閱本主題的＜備註＞一節，以取得詳細資訊。|  
|**strong_refcount**|**int**|這個**AppDomain**的強式參考數目。 這會反映使用此**AppDomain**的目前執行中批次數目。 請注意，執行此視圖將會建立**強式 refcount**;即使目前沒有正在執行的程式碼， **strong_refcount**的值會是1。|  
|**weak_refcount**|**int**|此**AppDomain**的弱式參考數目。 這表示要快取**AppDomain**內的多少個物件。 當您執行 managed 資料庫物件時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將它快取到**AppDomain**內，以供日後重複使用。 這樣可以提高執行效能。|  
|**cost**|**int**|**AppDomain**的成本。 成本愈高，就越可能在記憶體不足的壓力下卸載此**AppDomain** 。 成本通常取決於重新建立此**AppDomain**所需的記憶體數量。|  
|**value**|**int**|**AppDomain**的值。 值越低，就越可能在記憶體不足的壓力下卸載此**AppDomain** 。 值通常取決於使用此**AppDomain**的連接或批次數目。|  
|**total_processor_time_ms**|**bigint**|自處理序啟動以來，在目前應用程式定義域中執行之所有執行緒所用的處理器總時間 (以毫秒為單位)。 這相當於**MonitoringTotalProcessorTime**。|  
|**total_allocated_memory_kb**|**bigint**|自應用程式定義域建立以來，它所進行的所有記憶體配置總大小 (以 KB 為單位)，不減去已回收的記憶體。 這相當於**MonitoringTotalAllocatedMemorySize**。|  
|**survived_memory_kb**|**bigint**|在上次完整區塊回收中存活下來且已知為目前應用程式定義域所參考的 KB 數。 這相當於**MonitoringSurvivedMemorySize**。|  
  
## <a name="remarks"></a>備註  
 Dm_clr_appdomains 之間有一對一關聯性 **。 appdomain_address**和**dm_clr_loaded_assemblies appdomain_address**。  
  
 下表列出可能的**狀態值**、其描述，以及它們在**AppDomain**生命週期中發生的時間。 您可以使用這項資訊來追蹤**appdomain**的週期，並監看是否有可疑或重複的**appdomain**實例卸載，而不需要剖析 Windows 事件記錄檔。  
  
## <a name="appdomain-initialization"></a>AppDomain 初始化  
  
|State|描述|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|正在建立**AppDomain** 。|  
  
## <a name="appdomain-usage"></a>AppDomain 使用方式  
  
|State|描述|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|執行時間**AppDomain**已準備好供多個使用者使用。|  
|E_APPDOMAIN_SINGLEUSER|**AppDomain**已準備好在 DDL 作業中使用。 這些與 E_APPDOMAIN_SHARED 不同，因為共用的 AppDomains 是用於 CLR 整合執行，與 DDL 作業相反。 這類的 AppDomains 會與其他的並行作業隔離。|  
|E_APPDOMAIN_DOOMED|**AppDomain**已排程要卸載，但目前有線程在其中執行。|  
  
## <a name="appdomain-cleanup"></a>AppDomain 清除  
  
|State|描述|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已要求 CLR 卸載**AppDomain**，通常是因為包含 managed 資料庫物件的元件已改變或卸載。|  
|E_APPDOMAIN_UNLOADED|CLR 已卸載**AppDomain**。 這通常是因為**ThreadAbort**、 **OutOfMemory**或使用者程式碼中未處理的例外狀況而產生的問題。|  
|E_APPDOMAIN_ENQUEUE_DESTROY|已在 CLR 中卸載**AppDomain** ，並將其設定為終結 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|E_APPDOMAIN_DESTROY|**AppDomain**正在被終結的進程中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|E_APPDOMAIN_ZOMBIE|**Appdomain**已由終結， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不過，並非所有對**appdomain**的參考都已清除。|  
  
## <a name="permissions"></a>權限  
 需要資料庫的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何針對指定的元件來查看**AppDomain**的詳細資料：  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 下列範例顯示如何在指定的**AppDomain**中查看所有元件：  
  
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
 [dm_clr_loaded_assemblies &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [Common Language Runtime 相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
