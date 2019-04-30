---
title: 以指令碼編寫資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22fae65a5e62be579f751dd3d6d3d0c9a73e7409
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316400"
---
# <a name="script-a-table"></a>編寫資料表的指令碼
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可以建立指令碼來選取、插入、更新和刪除資料表，以及建立、變更、卸除或執行預存程序。  
  
 您有時會希望指令碼有多個選項，如先卸除程序，再建立程序，或先建立資料表，再變更資料表。 若要建立結合的指令碼，請將第一個指令碼儲存在 [查詢編輯器] 視窗中，再將第二個指令碼儲存在剪貼簿中，以便在視窗中將它貼在第一個指令碼之後。  
  
## <a name="creating-an-update-script"></a>建立更新指令碼  
  
#### <a name="to-create-the-insert-script-for-a-table"></a>建立資料表的插入指令碼  
  
1.  在物件總管中，展開您的伺服器，依序展開 [資料庫]、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 和 [資料表]，並以滑鼠右鍵按一下 [HumanResources.Employee]，然後指向 [產生資料表的指令碼為]。  
  
2.  快速鍵功能表有七個可用的指令碼選項：**若要建立**，**拖放到**， **DROP 並 CREATE 至**，**選取**，**插入到**，**更新**，並**刪除**。 指向 [UPDATE To]，然後按一下 [新增查詢編輯器視窗]。  
  
3.  此時會開啟新的 [查詢編輯器] 視窗、建立連接，並提供完整的 UPDATE 陳述式。  
  
     這個練習說明編寫指令碼的功能遠遠超過只是編寫建立資料表或預存程序的指令碼。 這項新功能可協助您將操作資料的指令碼快速加入專案中，以及輕鬆地編寫執行預存程序的指令碼。 如果資料表和程序有許多欄位，這可以節省很多時間。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [摘要：撰寫 TRANSACT-SQL](../../tutorials/summary-writing-transact-sql.md)  
  
  
