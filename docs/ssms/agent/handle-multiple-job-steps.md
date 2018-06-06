---
title: 處理多個作業步驟 | Microsoft Docs
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
- job steps [SQL Server Agent]
- ordering job steps [SQL Server]
- multiple job steps
- SQL Server Agent jobs, job steps
- control of flow for jobs [SQL Server]
ms.assetid: 7aba19ff-72b3-45f6-8e54-23f4988d63a8
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3b88a2d50bd748da3e56d43367706715fa4739f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="handle-multiple-job-steps"></a>處理多個作業步驟
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

如果您的作業有多重作業步驟，則必須指定這些作業步驟的執行順序。 這就叫做「流程控制」。 您可以加入新的作業步驟，並可隨時重新排列作業步驟的流程；變更內容將會在下次執行作業時生效。 下圖顯示資料庫備份作業的流程控制。  
  
![SQL Server Agent 作業步驟流程控制](../../ssms/agent/media/dbflow01.gif "SQL Server Agent 作業步驟流程控制")  
  
第一個步驟是「備份資料庫」。 如果這個步驟失敗了， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會向定義為接收通知的操作員報告失敗。 如果「備份資料庫」步驟成功，則作業會繼續進行下一個步驟：「刪除客戶資料」。 如果此步驟失敗，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會跳過，並進行「還原資料庫」。 如果「刪除客戶資料」成功，該作業會繼續下一個步驟「更新統計資料」等，直到最後一個步驟的結果為「報告成功」或「報告失敗」。  
  
您為每個作業步驟的成功與失敗定義一個流程控制動作。 您必須指定當作業步驟成功時所要執行的動作，以及作業步驟失敗時所要執行的動作。 您也可以定義作業步驟失敗時的重試次數和重試間隔。  
  
> [!NOTE]  
> 當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 圖形化使用者介面 (GUI)，並從多個步驟作業中刪除一或多個步驟時，GUI 會先移除所有作業步驟，然後再使用正確的 on-success 或 on-failure 參考，重新加入剩餘的步驟。 例如，假設您有一項包含五個步驟的作業，其中第一個步驟設定為若順利完成便跳到步驟 4。 如果您刪除步驟 3，GUI 便會移除此作業的所有步驟，並以更正過的參考加入剩餘的四個步驟 (步驟 1、2、4、5)。 在這個案例下，步驟 1 中的參考將會重新設定為如果步驟 1 順利完成便跳到步驟 3。  
  
作業步驟必須是各自獨立的。 也就是說，作業不能在作業步驟之間傳遞布林值、資料或數值。 但是，您可以使用永久性資料表或全域暫存資料表，將值從一個 [!INCLUDE[tsql](../../includes/tsql_md.md)] 作業步驟傳遞至另一個作業步驟。 您也可以使用檔案，將執行可執行程式之作業步驟中的值，從一個作業步驟傳遞到另一個作業步驟。 例如，由一個作業步驟所執行的可執行檔寫入檔案，再由後續作業步驟所執行的可執行檔來讀取檔案。  
  
> [!NOTE]  
> 如果您建立迴圈作業步驟 (作業步驟 1 之後接著作業步驟 2，然後作業步驟 2 再回到作業步驟 1)，當您使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]來建立作業時，會出現警告訊息。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會將作業及作業步驟資訊記錄在作業記錄中。  
  
## <a name="see-also"></a>另請參閱  
[sp_add_job](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
[sysjobs (Transact-SQL)](http://msdn.microsoft.com/en-us/e244a6a5-54c2-47a6-8039-dd1852b0ae59)  
[sysjobsteps](http://msdn.microsoft.com/en-us/978b8205-535b-461c-91f3-af9b08eca467)  
[實作作業](../../ssms/agent/implement-jobs.md)  
[管理作業步驟](../../ssms/agent/manage-job-steps.md)  
  
