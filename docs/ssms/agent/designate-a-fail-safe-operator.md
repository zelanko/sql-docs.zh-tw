---
title: 指定保全操作員
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- fail-safe operator [SQL Server]
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 0f4eb513-5c0a-4523-974e-e85c1deeb57f
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1c56acaa84b26192d766097294a5ab2bfd31ab8d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242454"
---
# <a name="designate-a-fail-safe-operator"></a>指定保全操作員
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

如果在無法聯繫到指定的操作員時，就會由保全操作員這位使用者接收警示。 本主題描述如何使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)]，以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中設定保全操作員來接收 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent 警示通知。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制事項  
  
-   呼叫器和 **net send** 選項會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來版本的 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
-   請注意，必須設定 SQL Server Agent 使用 Database Mail，才能將電子郵件及呼叫器通知傳送給操作員。 如需詳細資訊，請參閱＜ [指派警示給操作員](assign-alerts-to-an-operator.md)＞。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員才能指定保全操作員。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-designate-a-fail-safe-operator"></a>若要指定保全操作員  
  
1.  在物件總管  中，按一下加號，展開包含要指定為保全操作員之 SQL Server Agent 操作員的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]  ，然後選取 [屬性]  。  
  
3.  在 [SQL Server Agent 屬性 - _server\_name_] 對話方塊的 [選取頁面] 下，選取 [警示系統]。  
  
4.  在 [保全操作員]  下方，選取 [啟用保全操作員]  。  
  
5.  在 [操作員]  清單中，選取您想要設為保全操作員的操作員。  
  
6.  選取下列任何一個或所有核取方塊，指定通知操作員的方法：[電子郵件]  、[呼叫器]  或 [Net send]  。  
  
7.  完成後，請按一下 **[確定]** 。  
  
