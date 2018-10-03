---
title: 將目標伺服器編列至主要伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 298a3045cc9fc51664c77fcc28d89c95d30fd6fe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085628"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>將目標伺服器編列至主要伺服器
  此主題描述如何將目標伺服器新增至多伺服器管理組態。 從主要伺服器執行這個程序。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 SQL Server 管理物件 (SMO)。  
  
 如需有關用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務之 Windows 帳戶如何影響多伺服器環境的詳細資訊，請參閱 [建立多伺服器環境](create-a-multiserver-environment.md)。  
  
 依預設，主要伺服器和目標伺服器之間的連接會啟用完整的安全通訊端層 (SSL) 加密與憑證驗證。 如需詳細資訊，請參閱 [在目標伺服器上設定加密選項](set-encryption-options-on-target-servers.md)。  
  
 **本主題內容**  
  
-   **若要編列目標伺服器，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>若要編列目標伺服器  
  
1.  在 **[物件總管]** 中，展開設定為主要伺服器的伺服器。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]**，指向 **[多伺服器管理]**，然後按一下 **[新增目標伺服器]**。  
  
3.  完成「目標伺服器精靈」，精靈將引導您完成此程序。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>若要編列目標伺服器  
  
1.  使用 `sp_msx_enlist` 預存程序。  如需詳細資訊，請參閱 < [sp_msx_enlist &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
##  <a name="PowerShellProcedure"></a> 使用 SQL Server Management Objects (SMO)  
  
## <a name="see-also"></a>另請參閱  
 [將整個企業的管理自動化](automated-administration-across-an-enterprise.md)  
  
  
