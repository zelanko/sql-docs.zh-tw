---
title: SQL Server Agent 錯誤記錄檔 | Microsoft Docs
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
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 87b362a568a020f4882ebbed4b8e1e7558a6c3a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33042435"
---
# <a name="sql-server-agent-error-log"></a>SQL Server Agent 錯誤記錄檔
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 依預設，Agent 會建立錯誤記錄檔來記錄警告與錯誤。 記錄檔中會顯示下列警告和錯誤：  
  
-   提供有關潛在問題的警告訊息，例如「作業 \<*作業名稱*> 已於執行時刪除」。  
  
-   通常需要系統管理員介入的錯誤訊息，例如「無法啟動郵件工作階段」。 錯誤訊息可以藉由 **net send**來傳送給特定的使用者或電腦。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 至多可以維護九個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 錯誤記錄檔。 每個已封存之記錄檔的副檔名都會指出記錄檔的相對存在時間。 例如，.1 的副檔名表示它是最近新封存的錯誤記錄檔，而 .9 的副檔名則表示是最早封存的錯誤記錄檔。  
  
因為執行追蹤訊息會填滿 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 錯誤記錄檔，所以在預設情況下，並不會寫入錯誤記錄檔。 當錯誤記錄檔滿了，會降低您選取與分析更困難錯誤的能力。 因為記錄檔會增加伺服器的處理負擔，請務必仔細考慮將執行追蹤訊息擷取到錯誤記錄檔是否值得。 一般而言，最好只有在為一個特定問題進行偵錯時，您才擷取所有的訊息。  
  
當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 停止時，您可以修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 錯誤記錄檔的位置。 您無法開啟空的錯誤記錄檔。 您可以隨時循環使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 記錄檔，無須停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent。  
  
**若要檢視 SQL Server Agent 錯誤記錄檔**  
  
-   [檢視 SQL Server Agent 錯誤記錄檔 &#40;SQL Server Management Studio&#41;](../../ssms/agent/view-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**若要重新命名 SQL Server Agent 錯誤記錄檔**  
  
-   [重新命名 SQL Server Agent 錯誤記錄檔 &#40;SQL Server Management Studio&#41;](../../ssms/agent/rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**若要傳送 SQL Server Agent 錯誤訊息**  
  
-   [Send SQL Server Agent Error Messages](../../ssms/agent/send-sql-server-agent-error-messages.md)  
  
**若要將執行追蹤訊息寫入 SQL Server Agent 錯誤記錄檔**  
  
-   [在 SQL Server Agent 錯誤記錄檔中寫入執行追蹤訊息 &#40;SQL Server Management Studio&#41;](../../ssms/agent/write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
