---
title: 將目標伺服器的時鐘同步化
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7fa715d0df6c94630564ede8a162a940542d7510
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75257903"
---
# <a name="synchronize-target-server-clocks"></a>將目標伺服器的時鐘同步化

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，將 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的目標伺服器的時鐘與主要伺服器的時鐘進行同步處理。 同步處理這些系統時鐘可以支援您的作業排程。  

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>若要將目標伺服器的時鐘同步化  
  
1.  在 **[物件總管]** 中，按一下加號，展開要將目標伺服器的時鐘與主要伺服器的時鐘進行同步處理的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]  、指向 [多伺服器管理]  ，然後選取 [管理目標伺服器]  。  
  
3.  在 **[管理目標伺服器]** 對話方塊中，按一下 **[公佈指示]** 。  
  
4.  在 **[指示類型]** 清單中選取 **[同步處理時鐘]** 。  
  
5.  在 **[收件者]** 下，執行下列其中一項：  
  
    -   按一下 **[所有目標伺服器]** ，將所有目標伺服器的時鐘與主要伺服器的時鐘進行同步處理。  
  
    -   按一下 **[下列目標伺服器]** 以同步處理特定的伺服器時鐘，然後選取要與主要伺服器時鐘進行時鐘同步處理的每一部目標伺服器。  
  
6.  完成後，請按一下 **[確定]** 。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-synchronize-target-server-clocks"></a>若要將目標伺服器的時鐘同步化  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_resync_targetserver (Transact-SQL)](https://msdn.microsoft.com/40e44df7-d3e3-44ee-b149-08aba629a21f)。  
  
