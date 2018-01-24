---
title: "設定要在替代管道接聽的伺服器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
caps.latest.revision: "29"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: edc73b858a08ea0f8bda9e7a4d5ede8d2c05cccf
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe"></a>設定要在替代管道接聽的伺服器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 SQL Server 設定管理員，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定伺服器於替代管道接聽。 根據預設， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的預設執行個體會接聽具名管道 \\\\.\pipe\sql\query。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 與 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的具名執行個體會在其他管道上接聽。  
  
 有三種方式可利用用戶端應用程式連接到特定的具名管道：  
  
-   在伺服器上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。  
  
-   在用戶端上建立一個別名，指定具名管道。  
  
-   設定用戶端使用自訂連接字串進行連接。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>若要設定 SQL Server Database Engine 所使用的具名管道  
  
1.  在 SQL Server 組態管理員的主控台窗格中，展開 [SQL Server 網路組態]，然後按一下並展開 [\<執行個體名稱> 的通訊協定]。  
  
2.  在詳細資料窗格中，以滑鼠右鍵按一下 [具名管道]，然後按一下 [內容]。  
  
3.  在 **[通訊協定]** 索引標籤的 **[管道名稱]** 方塊中，輸入您要 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 接聽的管道，然後按一下 **[確定]**。  
  
4.  在主控台窗格中，按一下 **[SQL Server 服務]**。  
  
5.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server (\<執行個體名稱>)]，然後按一下 [重新啟動]，以停止並重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽替代管道時，有三種方式可利用用戶端應用程式連接到特定的具名管道：  
  
-   在伺服器上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。  
  
-   在用戶端上建立一個別名，指定具名管道。  
  
-   設定用戶端使用自訂連接字串進行連接。  
  
## <a name="see-also"></a>另請參閱  
 [建立或刪除用戶端使用的伺服器別名 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [伺服器網路組態](../../database-engine/configure-windows/server-network-configuration.md)  
  
  
