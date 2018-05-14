---
title: 設定作業記錄 | Microsoft Docs
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
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bad14efb03e320a810722a2c3ae590446570f9c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何設定 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 的作業記錄。  
  
-   **開始之前**  [安全性](#Security)  
  
-   **若要使用下列項目設定作業記錄：**[SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
**若要設定作業記錄**  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後按一下 [屬性]。  
  
3.  在 **[SQL Server Agent 屬性]** 對話方塊中，選取 **[記錄]** 頁面。  
  
4.  選擇下列選項：  
  
    1.  核取 **[限制作業記錄大小]**，然後輸入作業記錄的最大資料列數，以及每一個作業的最大資料列數。  
  
    2.  核取 **[自動移除代理程式記錄]**，並指定時間週期，比此週期要舊的記錄將會從記錄清除。  
  
## <a name="see-also"></a>另請參閱  
[實作作業](../../ssms/agent/implement-jobs.md)  
[監視作業活動](../../ssms/agent/monitor-job-activity.md)  
[建立作業](../../ssms/agent/create-jobs.md)  
  
