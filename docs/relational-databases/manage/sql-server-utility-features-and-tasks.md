---
title: SQL Server 公用程式的功能與工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 79f58c6bdcff4e3f43a7ef61457de40e371ab025
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686626"
---
# <a name="sql-server-utility-features-and-tasks"></a>SQL Server 公用程式的功能與工作
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客戶有一項需求，也就是以整體方式管理其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境，這項需求會在這一版中透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內應用程式和多伺服器管理的概念來滿足。  
  
## <a name="benefits-of-the-sql-server-utility"></a>SQL Server 公用程式的優點  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式會將組織的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相關實體在統一的檢視中模型化。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SSMS) 中的公用程式總管和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 公用程式視點會透過做為公用程式控制點 (UCP) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，為系統管理員提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源健全狀況的整體檢視。 UCP 中所呈現之使用量過低和使用量過高的原則以及各種索引鍵參數的摘要和詳細資料組合，將可讓您輕鬆識別資源合併機會和資源使用量過高的情形。 健全狀況原則是可以設定的，而且可加以調整來變更資源使用量的上下臨界值。 您可以變更全域監視原則，或是針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中管理的每個實體來設定個別監視原則。  
  
##  <a name="typical_scenarios"></a> SQL Server 公用程式使用者入門  
 一般使用者案例會從建立公用程式控制點開始，公用程式控制點會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的中央推理點。 UCP 會根據自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體收集到的資源健全狀況，提供合併檢視。 在建立 UCP 之後，您會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式，以便它們可以受到 UCP 的管理。  
  
 受到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式管理的每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和資料層應用程式都可以根據全域原則定義或個別原則定義來進行監視。  
  
## <a name="related-tasks"></a>相關工作  
 若要開始使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式，請使用下列主題。  
  
|||  
|-|-|  
|**描述**|**主題**|  
|描述設定伺服器在相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上執行公用程式和非公用程式收集組的考量。|[在相同 SQL Server 執行個體上執行公用程式和非公用程式收集組的考量事項](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|描述如何建立 SQL Server 公用程式控制點。|[建立 SQL Server 公用程式控制點 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|描述如何連接至 SQL Server 公用程式。|[連接至 SQL Server 公用程式](../../relational-databases/manage/connect-to-a-sql-server-utility.md)|  
|描述如何使用公用程式控制點來註冊 SQL Server 執行個體。|[註冊 SQL Server 的執行個體 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|描述如何使用公用程式總管來管理 SQL Server 公用程式。|[使用公用程式總管來管理 SQL Server 公用程式](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|描述如何在 SQL Server 公用程式中監視 SQL Server 執行個體。|[監視 SQL Server 公用程式中的 SQL Server 執行個體](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|描述如何檢視資源健全狀況原則結果。|[檢視資源健全狀況原則結果 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)|  
|描述如何修改資源健全狀況原則定義。|[修改資源健康情況原則定義 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|描述如何設定 UCP 資料倉儲。|[設定公用程式控制點資料倉儲 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|描述如何設定公用程式健全狀況原則。|[設定健全狀況原則 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)|  
|描述如何調整 CPU 使用量原則的衰減。|[降低 CPU 使用量原則的雜訊 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|描述如何移除 UCP 中的 SQL Server 執行個體。|[從 SQL Server 公用程式移除 SQL Server 執行個體](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|描述如何在 SQL Server 受管理的執行個體上變更公用程式資料收集器的 Proxy 帳戶。|[變更 SQL Server 受管理的執行個體上之公用程式收集組的 Proxy 帳戶 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|描述如何將 UCP 從某個 SQL Server 執行個體移至另一個 SQL Server 執行個體。|[將 UCP 從一個 SQL Server 執行個體移到另一個 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|描述如何移除 UCP。|[移除公用程式控制點 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/remove-a-utility-control-point-sql-server-utility.md)|  
|描述如何疑難排解 SQL Server 公用程式。|[疑難排解 SQL Server 公用程式](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)|  
|描述如何疑難排解 SQL Server 資源健全狀況。|[疑難排解 SQL Server 資源健全情況 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|UtilityExplorer F1 說明主題的連結。|[公用程式總管 F1 說明](../../relational-databases/manage/utility-explorer-f1-help.md)|  
  
  
