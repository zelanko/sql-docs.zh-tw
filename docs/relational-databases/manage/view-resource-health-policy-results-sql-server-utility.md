---
title: "檢視資源健全狀況原則結果 (SQL Server 公用程式) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2424c5e6ef2fe348c35f361b71927644aca590b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>檢視資源健全狀況原則結果 (SQL Server 公用程式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的公用程式儀表板，檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受控執行個體和資料層應用程式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資源參數。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="view-sql-server-utility-resource-health-policy-results"></a>檢視 SQL Server 公用程式資源健全狀況原則結果  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中，按一下 [檢視]，然後按一下 [公用程式總管]，檢視公用程式總管瀏覽窗格。 若要檢視此內容窗格，請按一下 **[檢視]**，然後按一下 **[公用程式總管內容]**。  
  
2.  在瀏覽窗格中，按一下 [連接到公用程式] ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")。 如果您尚未建立公用程式控制點 (UCP) 或是您尚未將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或資料層應用程式註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
3.  按一下 [UCP] 節點，檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體和資料層應用程式的摘要資料 (按一下滑鼠右鍵重新整理)。 儀表板資料會顯示在內容窗格中。  
  
4.  按一下 [受管理的執行個體] 節點，檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理執行個體的清單檢視資料 (按一下滑鼠右鍵重新整理)。 清單檢視資料會顯示在內容窗格中。  
  
5.  按一下 [部署的資料層應用程式] 節點，檢視資料層應用程式的清單檢視資料 (按一下滑鼠右鍵重新整理)。 清單檢視資料會顯示在內容窗格中。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [降低 CPU 使用量原則的雜訊 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)   
 [部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)   
 [受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)   
 [公用程式管理 &#40;SQL Server 公用程式&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)  
  
  
