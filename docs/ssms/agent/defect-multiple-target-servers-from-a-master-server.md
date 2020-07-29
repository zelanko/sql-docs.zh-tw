---
title: Defect Multiple Target Servers from a Master Server
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dc813e464e56139e81eb052f497b16f472829a1a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775123"
---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>Defect Multiple Target Servers from a Master Server

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的多伺服器管理組態中脫離多個目標伺服器。 從主要伺服器執行這個程序。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>若要從主要伺服器脫離多個目標伺服器  
  
1.  在 **[物件總管]** 中，展開設定為主要伺服器的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]  ，指向 [多重伺服器管理]  ，然後按一下 [管理目標伺服器]  。  
  
3.  按一下 **[公佈指示]** ，然後在 **[指示類型]** 清單中選取 **[脫離]** 。  
  
4.  在 **[收件者]** 下，執行下列其中一項：  
  
    -   按一下 **[所有目標伺服器]** ，脫離此主要伺服器的所有目標伺服器。 如果您要完整解除安裝目前的多伺服器管理組態，請使用此選項。  
  
    -   按一下 **[下列目標伺服器]** ，然後按一下對應的 **[選取]** 方塊，脫離此主要伺服器的部份目標伺服器，但不是所有目標伺服器。  
  
## <a name="see-also"></a>另請參閱  
[建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[使目標伺服器脫離主要伺服器](../../ssms/agent/defect-a-target-server-from-a-master-server.md)  
  
