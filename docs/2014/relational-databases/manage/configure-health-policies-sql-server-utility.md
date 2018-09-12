---
title: 設定健康狀態原則 (SQL Server 公用程式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 030aac3b-8901-4c41-91ed-aba96420276c
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a24e20fc9f371fee09d45c4724c277c691a7b6c6
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809734"
---
# <a name="configure-health-policies-sql-server-utility"></a>設定健康情況原則 (SQL Server 公用程式)
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 公用程式儀表板，針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體和資料層應用程式檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資源參數。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)。  
  
 若要檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式健全狀況原則結果，請從 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]連接到公用程式控制點。 如需詳細資訊，請參閱 [使用公用程式總管來管理 SQL Server 公用程式](use-utility-explorer-to-manage-the-sql-server-utility.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以針對資料層應用程式和受管理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體來設定公用程式健全狀況原則。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內針對所有資料層應用程式和受管理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來以全域方式定義健全狀況原則，或者可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內針對每一個資料層應用程式及每一個受管理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來個別定義健全狀況原則。  
  
## <a name="monitoring-policies-for-data-tier-applications"></a>監視資料層應用程式的原則  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料層應用程式的使用量過高和使用量過低原則如下：  
  
-   資料層應用程式的處理器使用率。  
  
-   適用於資料庫檔案的資料層應用程式檔案空間。  
  
-   適用於存放磁碟區的資料層應用程式檔案空間。  
  
-   電腦處理器使用率。  
  
> [!NOTE]  
>  對於資料層應用程式而言，存放磁碟區和處理器使用率是唯讀原則。  
  
 如需有關檢視或變更資料層應用程式之全域監視原則的詳細資訊，請參閱[公用程式管理 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-administration-sql-server-utility.md)。  
  
 如需有關檢視或變更個別資料層應用程式監視原則的詳細資訊，請參閱[部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)。  
  
## <a name="monitoring-policies-for-managed-instances-of-sql-server"></a>SQL Server Managed 執行個體的監視原則  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體的使用量過高和使用量過低原則如下：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體處理器使用率。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檔案空間。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體檔案空間。  
  
-   電腦處理器使用率。  
  
 如需有關檢視或變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體之全域監視原則的詳細資訊，請參閱[公用程式管理 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-administration-sql-server-utility.md)。  
  
 如需有關檢視或變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 個別受管理的執行個體之監視原則的詳細資訊，請參閱[受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)   
 [降低 CPU 使用量原則的雜訊 &#40;SQL Server 公用程式&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
  
