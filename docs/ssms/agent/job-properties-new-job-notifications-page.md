---
title: 作業屬性 - 新增作業 (通知頁面)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2d1bc2ec3aef699e491fdac2036352fd986fec85
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85690606"
---
# <a name="job-properties---new-job-notifications-page"></a>作業屬性 - 新增作業 (通知頁面)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來設定當作業完成時，[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要執行的動作。  
  
## <a name="options"></a>選項。  
**電子郵件**  
選取此選項，即可在作業完成時傳送電子郵件。 在選取此選項後，請選擇要通知之操作員及觸發通知的條件：[當作業成功時]  ；[當作業失敗時]  ；或 [當作業完成時]  。  
  
**頁面**  
選取此選項，即可在作業完成時將電子郵件傳送給操作員的呼叫器。 在選取此選項後，請指定要通知之操作員及觸發通知的條件：[當作業成功時]  ；[當作業失敗時]  ；或 [當作業完成時]  。  
  
**Net Send**  
選取此選項，即可在作業完成時使用 Net Send 來通知操作員。 在選取此選項後，請指定要通知之操作員及觸發通知的條件：[當作業成功時]  ；[當作業失敗時]  ；或 [當作業完成時]  。  
  
**寫入 Windwos 應用程式事件記錄**  
選取此選項，即可在作業完成時將項目寫入應用程式事件記錄檔。 在選取此選項後，請指定會造成寫入項目的條件：[當作業成功時]  ；[當作業失敗時]  ；或 [當作業完成時]  。  
  
**自動刪除作業**  
選取此選項，即可在作業完成時刪除作業。 在選取此選項後，請指定會觸發刪除作業的條件：[當作業成功時]  ；[當作業失敗時]  ；或 [當作業完成時]  。  
  
## <a name="see-also"></a>另請參閱  
[實作作業](../../ssms/agent/implement-jobs.md)  
[操作說明：設定 SQL Server Agent Mail 使用 Database Mail](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
