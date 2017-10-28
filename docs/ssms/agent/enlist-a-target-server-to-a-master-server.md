---
title: "將目標伺服器編列至主要伺服器 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 61fb82bcd0f3ac4308e023e31338f8142614488d
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="enlist-a-target-server-to-a-master-server"></a>將目標伺服器編列至主要伺服器
此主題描述如何將目標伺服器新增至多伺服器管理組態。 從主要伺服器執行這個程序。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、 [!INCLUDE[tsql](../../includes/tsql_md.md)]或 SQL Server 管理物件 (SMO)。  
  
如需有關用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務之 Windows 帳戶如何影響多伺服器環境的詳細資訊，請參閱 [建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)。  
  
依預設，主要伺服器和目標伺服器之間的連接會啟用完整的安全通訊端層 (SSL) 加密與憑證驗證。 如需詳細資訊，請參閱 [在目標伺服器上設定加密選項](../../ssms/agent/set-encryption-options-on-target-servers.md)。  
  
**本主題內容**  
  
-   **若要編列目標伺服器，使用：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>若要編列目標伺服器  
  
1.  在 **[物件總管]**中，展開設定為主要伺服器的伺服器。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]**，指向 **[多伺服器管理]**，然後按一下 **[新增目標伺服器]**。  
  
3.  完成「目標伺服器精靈」，精靈將引導您完成此程序。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>若要編列目標伺服器  
  
1.  **sp_msx_enlist** 預存程序會編輯登錄。  如需詳細資訊，請參閱 [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
## <a name="see-also"></a>另請參閱  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  

