---
description: 使用效能物件
title: 使用效能物件
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 372390ed9f6c893c1762ca635e5aa9b5f3e3c9ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480240"
---
# <a name="use-performance-objects"></a>使用效能物件
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 包含效能物件及計數器，可用來監視服務執行的狀況。 這些效能物件可讓您使用「效能監視器」(一種 Windows 工具)，來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務在背景執行哪些工作。 例如，您可以識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務目前正在執行多少使用中的作業，以找出被封鎖的作業。  
  
針對電腦上所安裝的每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，都有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務效能物件及計數器存在。 效能物件是依據每項物件所代表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來命名的。  
  
下表顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務效能物件的命名方式：  
  
|執行個體類型|物件名稱|  
|-----------------|---------------|  
|預設|**SQLAgent:**_object_:_counter_|  
|已命名|**SQLAgent$**<br /> **&#42;instance_name&#42; :**_object_:_counter_|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的下列效能物件。  
  
|物件名稱|描述|  
|---------------|---------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|有關已啟動作業、成功率及目前狀態的效能資訊|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|作業步驟的狀態資訊|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|警示及通知數的相關資訊|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|一般效能資訊|  
  
## <a name="see-also"></a>另請參閱  
[效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
[如何：啟動系統監視器 (Windows)](https://msdn.microsoft.com/5e51bb79-5737-470b-9c47-fac330c001c5)  
  
