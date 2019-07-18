---
title: 第 2 課：準備快照集資料夾 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5ec45b0a29f9f4c8fb1e6a9b683e47797f194885
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721019"
---
# <a name="lesson-2-preparing-the-snapshot-folder"></a>第 2 課：準備快照集資料夾
  在這一課，您將學習設定用於建立及儲存發行集快照集的快照集資料夾。  
  
### <a name="to-create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>建立快照集資料夾的共用並指定權限  
  
1.  在 [Windows 檔案總管] 中，導覽到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的資料夾。 預設位置是 C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data。  
  
2.  建立名為 **repldata** 的新資料夾。  
  
3.  以滑鼠右鍵按一下該資料夾，然後按一下 [內容]。  
  
4.  在 [repldata 內容] 對話方塊的 [共用] 索引標籤上，按一下 [共用]。  
  
5.  在 [檔案共用] 對話方塊中，按一下 [共用]，然後按一下 [完成]。  
  
6.  在 **[安全性]** 索引標籤上，按一下 **[編輯]**。  
  
7.  在 [權限] 對話方塊中，按一下 [新增]。 在 [選取使用者、電腦、服務帳戶或群組] 文字方塊中，輸入第 1 課所建立的快照集代理程式帳戶名稱，如 \<_電腦名稱>_**\repl_snapshot**，其中 \<*電腦名稱>* 是「發行者」的名稱。 按一下 [檢查名稱]，然後按一下 [確定]。  
  
8.  重複上一個步驟，為散發代理程式 \<_電腦名稱>_**\repl_distribution** 以及合併代理程式 \<_電腦名稱>_**\repl_merge** 新增權限。  
  
9. 確認允許下列權限；  
  
    -   repl_snapshot - Full Control  
  
    -   repl_distribution - Read  
  
    -   repl_merge - Read  
  
10. 按一下 [確定] 關閉 [repldata 屬性] 對話方塊，並建立 repldata 共用。  
  
## <a name="next-steps"></a>後續步驟  
 您已順利設定快照集資料夾的共用。 下一步，您將設定散發。 請參閱[第 3 課：設定散發](lesson-3-configuring-distribution.md)。  
  
## <a name="see-also"></a>另請參閱  
 [保護快照集資料夾](security/secure-the-snapshot-folder.md)  
  
  
