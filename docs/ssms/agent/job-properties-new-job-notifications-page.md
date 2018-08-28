---
title: 作業屬性 - 新增作業 (通知頁面) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 60f26b4d026b8fd0e88ee5db40af027fdb2dfffd
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42776585"
---
# <a name="job-properties---new-job-notifications-page"></a>作業屬性 - 新增作業 (通知頁面)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來設定當作業完成時，[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要執行的動作。  
  
## <a name="options"></a>選項。  
**電子郵件**  
選取此選項，即可在作業完成時傳送電子郵件。 選取此選項之後，請選擇要通知的操作員及觸發通知的條件：[當作業成功時]、[當作業失敗時] 或 [作業完成時]。  
  
**頁面**  
選取此選項，即可在作業完成時將電子郵件傳送給操作員的呼叫器。 選取此選項之後，請指定要通知的操作員及觸發通知的條件：[當作業成功時]、[當作業失敗時] 或 [作業完成時]。  
  
**Net Send**  
選取此選項，即可在作業完成時使用 Net Send 來通知操作員。 選取此選項之後，請指定要通知的操作員及觸發通知的條件：[當作業成功時]、[當作業失敗時] 或 [作業完成時]。  
  
**寫入 Windwos 應用程式事件記錄**  
選取此選項，即可在作業完成時將項目寫入應用程式事件記錄檔。 選取此選項之後，請指定寫入項目時的條件：[當作業成功時]、[當作業失敗時] 或 [作業完成時]。  
  
**自動刪除作業**  
選取此選項，即可在作業完成時刪除作業。 選取此選項之後，請指定觸發刪除作業的條件：[當作業成功時]、[當作業失敗時] 或 [作業完成時]。  
  
## <a name="see-also"></a>另請參閱  
[實作作業](../../ssms/agent/implement-jobs.md)  
[如何：將 SQL Server Agent Mail 設定為使用 Database Mail (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
