---
title: 管理整個企業的作業 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 135f6e037e71e9af94bc5f6db21782d17713ec31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65105432"
---
# <a name="manage-jobs-across-an-enterprise"></a>管理整個企業的作業
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

如果您在 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 以外對多伺服器作業定義做了變更，則您必須將變更公佈到下載清單，以便目標伺服器可以再次下載已更新的作業。 若要確保目標伺服器具有目前的作業定義，請在更新多伺服器作業後公佈 INSERT 指示，如下所示：  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
若要通知目標伺服器多伺服器作業已有修改，您必須在使用下列任一程序後，叫用先前的命令：  
  
-   [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_update_jobstep (Transact-SQL)](https://msdn.microsoft.com/e158802c-c347-4a5d-bf75-c03e5ae56e6b)  
  
-   [sp_delete_jobstep (Transact-SQL)](https://msdn.microsoft.com/421ede8e-ad57-474a-9fb9-92f70a3e77e3)  
  
-   [管理事件](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
-   [sp_detach_schedule (Transact-SQL)](https://msdn.microsoft.com/9a1fc335-1bef-4638-a33a-771c54a5dd19)  
  
    > [!NOTE]  
    > 在您呼叫 **sp_update_job** 或 **sp_delete_job** 之後，不需要呼叫 **sp_post_msx_operation**，因為這些預存程序會自動將所需的變更傳送到下載清單。  
  
下列是管理整個企業作業的一般工作。  
  
**若要檢查目標伺服器的狀態**  
  
-   [Transact-SQL](https://msdn.microsoft.com/f841d3bd-901a-4980-ad0b-1c6eeba3f717)  
  
-   [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**若要變更作業的目標伺服器**  
  
-   [Transact-SQL](../../ssms/agent/modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
-   [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**若要變更目標伺服器的位置**  
  
-   [Transact-SQL](../../ssms/agent/specify-a-target-server-s-location-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
-   [SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**若要將目標伺服器的時鐘同步化**  
  
-   [Transact-SQL](../../ssms/agent/synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/40e44df7-d3e3-44ee-b149-08aba629a21f)  
  
**若要強制目標伺服器輪詢主要伺服器**  
  
-   [Transact-SQL](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>另請參閱  
[管理事件](../../ssms/agent/manage-events.md)  
  
