---
title: 使目標伺服器脫離主要伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f7d83a7904f3b3d8f77f8ded6d4a30a88314a38e
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67688061"
---
# <a name="defect-a-target-server-from-a-master-server"></a>使目標伺服器脫離主要伺服器
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理物件 (SMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中從主伺服器脫離目標伺服器。 請從目標伺服器執行這個程序。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [安全性](#Security)  
  
-   **使用下列方法脫離目標伺服器：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SMO](#PowerShellProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>安全性  
  
#### <a name="Permissions"></a>Permissions  
若要執行這個預存程序，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>若要使目標伺服器脫離主伺服器  
  
1.  在 **[物件總管]** 中，展開設定為目標伺服器的伺服器。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]** ，指向 **[多伺服器管理]** ，然後按一下 **[脫離]** 。  
  
3.  按一下 **[是]** 以確定您要從主要伺服器脫離這台目標伺服器。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>若要使目標伺服器脫離主伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
```  
sp_msx_defect ;  
```  
  
如需詳細資訊，請參閱 [sp_msx_defect (Transact-SQL)](https://msdn.microsoft.com/0dfd963a-3bc5-4b58-94f7-aec976da2883)。  
  
## <a name="PowerShellProcedure"></a>使用 SQL Server 管理物件 (SMO)  
使用 **MsxDefect 方法**。  
  
## <a name="see-also"></a>另請參閱  
[建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[從主要伺服器脫離多個目標伺服器](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  
