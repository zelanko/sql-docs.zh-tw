---
title: 作業屬性 - 新增作業 (排程頁面) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.schedules.f1
ms.assetid: 0b03585b-a510-484d-8a63-9b32459def9c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4d9d06def940d757e183b2ed6341d034628ccea7
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267819"
---
# <a name="job-properties---new-job-schedules-page"></a>作業屬性 - 新增作業 (排程頁面)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

使用此頁面來檢視和組織 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的排程。  
  
## <a name="options"></a>選項。  
**排程清單**  
列出此作業的排程。  
  
**新增**  
建立新排程。 建立排程之後，該排程隨即加入作業中。  
  
**挑選**  
從現有的排程中選取排程。 因為作業和排程必須有相同的擁有者，所以此選項只允許從您個人擁有的排程中進行挑選。  
  
**編輯**  
編輯選取的排程，以變更作業排程屬性。  
  
**移除**  
從作業中移除選取的排程。 如果沒有其他作業使用排程，該排程將從資料庫中刪除。  
  
## <a name="see-also"></a>另請參閱  
[實作作業](../../ssms/agent/implement-jobs.md)  
  
