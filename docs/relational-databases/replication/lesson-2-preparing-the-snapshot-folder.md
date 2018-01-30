---
title: "第 2 課：準備快照集資料夾 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 969aca3b97e12f5a179c9f2fb4c748d93d89c760
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="lesson-2-preparing-the-snapshot-folder"></a>第 2 課：準備快照集資料夾
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 在這一課，您將學習設定用於建立及儲存發行集快照集的快照集資料夾。  
  
### <a name="to-create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>建立快照集資料夾的共用並指定權限  
  
1.  在 [Windows 檔案總管] 中，導覽到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的資料夾。 預設位置是 C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data。  
  
2.  建立名為 **repldata** 的新資料夾。  
  
3.  以滑鼠右鍵按一下該資料夾，然後按一下 [內容]。  
  
4.  在 [repldata 內容] 對話方塊的 [共用] 索引標籤上，按一下 [共用]。  
  
5.  在 [檔案共用] 對話方塊中，按一下 [共用]，然後按一下 [完成]。  
  
6.  在 **[安全性]** 索引標籤上，按一下 **[編輯]**。  
  
7.  在 [權限] 對話方塊中，按一下 [新增]。 在 [選取使用者、電腦、服務帳戶或群組] 文字方塊中，鍵入第 1 課所建立的快照集代理程式帳戶名稱，如 \<電腦名稱>****\repl_snapshot**，其中 \<電腦名稱>** 是「發行者」的名稱。 按一下 [檢查名稱]，然後按一下 [確定]。  
  
8.  重複上一個步驟，為散發代理程式 \<電腦名稱>****\repl_distribution** 以及合併代理程式 \<電腦名稱>****\repl_merge** 新增權限。  
  
9. 確認允許下列權限；  
  
    -   repl_snapshot - Full Control  
  
    -   repl_distribution - Read  
  
    -   repl_merge - Read  
  
10. 按一下 [確定] 關閉 [repldata 屬性] 對話方塊，並建立 repldata 共用。  
  
## <a name="next-steps"></a>Next Steps  
您已順利設定快照集資料夾的共用。 下一步，您將設定散發。 請參閱 [第 3 課：設定散發](../../relational-databases/replication/lesson-3-configuring-distribution.md)。  
  
## <a name="see-also"></a>另請參閱  
[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
  
