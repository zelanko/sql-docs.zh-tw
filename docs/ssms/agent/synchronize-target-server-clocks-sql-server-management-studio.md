---
title: "同步處理目標伺服器時鐘 (SQL Server Management Studio) | Microsoft Docs"
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
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cacbf8f58717dca6613810ab0b90edcca0df4c83
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>同步處理目標伺服器時鐘 (SQL Server Management Studio)
此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ，將 [!INCLUDE[tsql](../../includes/tsql_md.md)]中的目標伺服器的時鐘與主要伺服器的時鐘進行同步處理。 同步處理這些系統時鐘可以支援您的作業排程。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要使用下列項目將目標伺服器的時鐘同步處理：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>若要將目標伺服器的時鐘同步化  
  
1.  在 **[物件總管]** 中，按一下加號，展開要將目標伺服器的時鐘與主要伺服器的時鐘進行同步處理的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]、指向 [多伺服器管理]，然後選取 [管理目標伺服器]。  
  
3.  在 **[管理目標伺服器]** 對話方塊中，按一下 **[公佈指示]**。  
  
4.  在 **[指示類型]** 清單中選取 **[同步處理時鐘]**。  
  
5.  在 **[收件者]**下，執行下列其中一項：  
  
    -   按一下 **[所有目標伺服器]** ，將所有目標伺服器的時鐘與主要伺服器的時鐘進行同步處理。  
  
    -   按一下 **[下列目標伺服器]** 以同步處理特定的伺服器時鐘，然後選取要與主要伺服器時鐘進行時鐘同步處理的每一部目標伺服器。  
  
6.  完成後，請按一下 **[確定]**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-synchronize-target-server-clocks"></a>若要將目標伺服器的時鐘同步化  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_resync_targetserver (Transact-SQL)](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f)。  
  

