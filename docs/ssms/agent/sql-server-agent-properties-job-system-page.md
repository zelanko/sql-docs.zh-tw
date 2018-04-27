---
title: SQL Server Agent 屬性 (作業系統頁面) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8137d468fc55ed13ffd21a8a2770158aefcee018
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-agent-properties-job-system-page"></a>SQL Server Agent 屬性 (作業系統頁面)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來檢視和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務管理作業的方式。  
  
## <a name="options"></a>選項。  
**關機逾時間隔 (以秒為單位)**  
指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在關機之前，要等候作業完成的秒數。 如果在指定的時間間隔之後作業仍在執行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 就會強制停止作業。  
  
**使用非管理員 Proxy 帳戶**  
設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 的非管理員 Proxy 帳戶。 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 和更新的版本支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]Agent 版本時，才可以使用此選項。  
  
**User name**  
輸入非管理員 Proxy 帳戶的使用者名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]Agent 版本時，才可以使用此選項。  
  
**密碼**  
輸入非管理員 Proxy 帳戶的使用者密碼。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 和更新的版本支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 之前的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]Agent 版本時，才可以使用此選項。  
  
**網域**  
輸入非系統管理 Proxy 帳戶的使用者網域。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]Agent 版本時，才可以使用此選項。  
  
## <a name="see-also"></a>另請參閱  
[實作作業](../../ssms/agent/implement-jobs.md)  
  
