---
title: 作業屬性 - 新增作業 (一般頁面)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.general.f1
ms.assetid: b6832840-1c18-4db8-94fc-080db880ae9f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eeb3b97ab94c9510ae66b3ebf6c018799dcf07a1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764129"
---
# <a name="job-properties---new-job-general-page"></a>作業屬性 - 新增作業 (一般頁面)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來檢視和修改 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的一般屬性。  
  
## <a name="options"></a>選項。  
**名稱**  
變更作業的名稱。  
  
**擁有者**  
選取作業的擁有者。  
  
**類別目錄**  
選取作業的作業類別目錄。  
  
**...**  
檢視選取之類別目錄中的作業。  
  
**說明**  
變更作業的描述。  
  
**已啟用**  
啟用作業。 未啟用作業時，則不會執行作業以回應排程或警示，但是您仍可以使用 **sp_start_job** 預存程序來啟動作業。  
  
**Source**  
顯示作業的主要伺服器。 只能在 [作業屬性] 的 [一般]  頁面使用。  
  
**建立日期**  
顯示作業的建立日期和時間。 只能在 [作業屬性] 的 [一般]  頁面使用。  
  
**上次修改**  
顯示作業的上次修改日期和時間。 只能在 [作業屬性] 的 [一般]  頁面使用。  
  
**上次執行**  
顯示作業上次開始執行的日期和時間。 只能在 [作業屬性] 的 [一般]  頁面使用。  
  
**檢視作業記錄**  
檢視作業的作業記錄。 只能在 [作業屬性] 的 [一般]  頁面使用。  
  
## <a name="see-also"></a>另請參閱  
[實作作業](../../ssms/agent/implement-jobs.md)  
[作業類別目錄 - 管理作業類別目錄](../../ssms/agent/job-categories-manage-job-categories.md)  
  
