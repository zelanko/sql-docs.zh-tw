---
title: 處理多個作業步驟 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- ordering job steps [SQL Server]
- multiple job steps
- SQL Server Agent jobs, job steps
- control of flow for jobs [SQL Server]
ms.assetid: 7aba19ff-72b3-45f6-8e54-23f4988d63a8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 379877d3a08c60a293b96c5c57d55a2894ba0a79
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63074046"
---
# <a name="handle-multiple-job-steps"></a>處理多個作業步驟
  如果您的作業有多重作業步驟，則必須指定這些作業步驟的執行順序。 這就叫做「流程控制」。** 您可以加入新的作業步驟，並可隨時重新排列作業步驟的流程；變更內容將會在下次執行作業時生效。 下圖顯示資料庫備份作業的流程控制。  
  
 ![SQL Server Agent 作業步驟流程控制](../../database-engine/media/dbflow01.gif "SQL Server Agent 作業步驟流程控制")  
  
 第一個步驟是「備份資料庫」。 如果這個步驟失敗了， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會向定義為接收通知的操作員報告失敗。 如果「備份資料庫」步驟成功，則作業會繼續進行下一個步驟：「刪除客戶資料」。 如果此步驟失敗，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 會跳過，並進行「還原資料庫」。 如果「刪除客戶資料」成功，該作業會繼續下一個步驟「更新統計資料」等，直到最後一個步驟的結果為「報告成功」或「報告失敗」。  
  
 您為每個作業步驟的成功與失敗定義一個流程控制動作。 您必須指定當作業步驟成功時所要執行的動作，以及作業步驟失敗時所要執行的動作。 您也可以定義作業步驟失敗時的重試次數和重試間隔。  
  
> [!NOTE]  
>  當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 圖形化使用者介面 (GUI)，並從多個步驟作業中刪除一或多個步驟時，GUI 會先移除所有作業步驟，然後再使用正確的 on-success 或 on-failure 參考，重新加入剩餘的步驟。 例如，假設您有一項包含五個步驟的作業，其中第一個步驟設定為若順利完成便跳到步驟 4。 如果您刪除步驟 3，GUI 便會移除此作業的所有步驟，並以更正過的參考加入剩餘的四個步驟 (步驟 1、2、4、5)。 在這個案例下，步驟 1 中的參考將會重新設定為如果步驟 1 順利完成便跳到步驟 3。  
  
 作業步驟必須是各自獨立的。 也就是說，作業不能在作業步驟之間傳遞布林值、資料或數值。 但是，您可以使用永久性資料表或全域暫存資料表，將值從一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟傳遞至另一個作業步驟。 您也可以使用檔案，將執行可執行程式之作業步驟中的值，從一個作業步驟傳遞到另一個作業步驟。 例如，由一個作業步驟所執行的可執行檔寫入檔案，再由後續作業步驟所執行的可執行檔來讀取檔案。  
  
> [!NOTE]  
>  如果您建立迴圈作業步驟 (作業步驟 1 之後接著作業步驟 2，然後作業步驟 2 再回到作業步驟 1)，當您使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來建立作業時，會出現警告訊息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會將作業及作業步驟資訊記錄在作業記錄中。  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_job &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)   
 [sysjobhistory &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobhistory-transact-sql)   
 [sysjobs &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobs-transact-sql)   
 [sysjobsteps &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobsteps-transact-sql)   
 [執行作業](implement-jobs.md)   
 [管理作業步驟](manage-job-steps.md)  
  
  
