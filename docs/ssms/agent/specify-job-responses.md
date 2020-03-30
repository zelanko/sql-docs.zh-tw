---
title: 指定作業回應
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3208c2543292fd67ec36ad25dd5a065e08988ca6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245792"
---
# <a name="specify-job-responses"></a>指定作業回應
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

作業回應可指定完成作業後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式服務將採取的動作。 作業回應可確保資料庫管理員知道作業已完成，以及作業的執行頻率。 典型的作業回應包括：  
  
-   使用電子郵件、電子呼叫或 **net send** 訊息通知操作員。  
  
    如果操作員必須執行後續動作，請使用其中一個作業回應。 例如，如果備份作業成功完成，必須告知操作員以取下備份磁帶，並將其存放在安全的地方。  
  
-   將事件訊息寫入至 Windows 應用程式記錄。  
  
    這個回應只用於失敗的作業。  
  
-   自動刪除作業。  
  
    如果確定您將不再需要重新執行這個作業，請使用這個作業回應。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何通知操作員作業狀態。|[Notify an Operator of Job Status](../../ssms/agent/notify-an-operator-of-job-status.md)|  
|描述如何將作業狀態寫入 Windows 應用程式記錄檔。|[若要將作業狀態寫入到 Windows 應用程式記錄](../../ssms/agent/write-the-job-status-to-the-windows-application-log.md)|  
  
## <a name="see-also"></a>另請參閱  
[監視及回應事件](../../ssms/agent/monitor-and-respond-to-events.md)  
  
