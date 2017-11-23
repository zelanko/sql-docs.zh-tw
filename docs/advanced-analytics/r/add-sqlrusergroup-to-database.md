---
title: "為資料庫使用者加入 SQLRUserGroup |Microsoft 文件"
ms.custom: 
ms.date: 11/13/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "隱含的驗證"
- SQLRUserGroup
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 97a571a9a91ac31e955f6833e27a975f87267218
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>新增 SQLRUserGroup 為資料庫使用者

在安裝期間[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]或[!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]，以執行作業的安全性 token 底下建立新的 Windows 使用者帳戶[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]服務。 當使用者傳送的機器學習指令碼從外部用戶端，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟動可用工作者帳戶、 將它對應至在呼叫的使用者的身分識別和執行指令碼代表使用者。 Database engine 的這個新服務支援安全執行外部指令碼，呼叫*隱含的驗證*。

您可以檢視這些帳戶中的 Windows 使用者群組**SQLRUserGroup**。 根據預設，會建立 20 個背景工作帳戶，這通常是超過不足以執行 R 工作。

不過，如果您需要從遠端資料科學用戶端執行 R 指令碼，並使用 Windows 驗證，您必須授與這些背景工作帳戶登入的權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代替您執行個體。

## <a name="add-sqlrusergroup-as-a-sql-server-login"></a>新增 SQLRUserGroup 做為 SQL Server 登入

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，展開 [安全性] ，以滑鼠右鍵按一下 [登入] ，然後選取 [新增登入] 。

2. 在**登入-新增**對話方塊中，選取**搜尋**。 (沒有任何項目 方塊中輸入尚未。）
    
     ![按一下 搜尋来加入新的登入機器學習](media/implied-auth-login1.png "按一下要加入新的登入機器學習的搜尋")

3. 在**選取使用者或群組**方塊中，按一下**物件類型** 按鈕。

     ![搜尋要加入新的登入機器學習的物件類型](media/implied-auth-login2.png "搜尋要加入新的登入機器學習的物件類型")

4. 在**物件類型**對話方塊中，選取**群組**。 清除其他所有核取方塊。

     ![在 [物件類型] 對話方塊中選取群組](media/implied-auth-login3.png "物件類型 對話方塊中選取的群組")

4. 按一下**進階**，確認要搜尋的位置是目前的電腦，然後按一下**立即尋找**。

     ![按一下 [立即尋找]，取得群組清單](media/implied-auth-login4.png "按一下 [立即尋找]，取得群組清單")

5. 捲動清單，直到您找到一開始在伺服器上的群組帳戶的`SQLRUserGroup`。
    
    + 群組為 Launchpad 服務相關聯的名稱_預設執行個體_只是一律**SQLRUserGroup**。 選取此帳戶僅針對預設執行個體。
    + 如果您使用_具名執行個體_，執行個體名稱會附加至的預設名稱`SQLRUserGroup`。 因此，如果您的執行個體的名稱為"MLTEST"，這個執行個體的預設使用者群組名稱會是**SQLRUserGroupMLTest**。
 
     ![範例伺服器上的群組](media/implied-auth-login5.png "範例伺服器上的群組")
   
5. 按一下**確定**以關閉 [進階的搜尋] 對話方塊。

    > [!IMPORTANT]
    > 請確定您已選取正確的帳戶，執行個體。 每個執行個體可以使用只有自己 Launchpad 服務並為該服務建立的群組。 執行個體無法共用 Launchpad 服務或背景工作帳戶。

6. 按一下**確定**以關閉 [**選取使用者或群組**] 對話方塊。

7. 在**登入-新增**對話方塊中，按一下 **確定**。 依預設，登入指派給 **公用** 角色，並有連接到資料庫引擎的權限。

## <a name="change-the-number-of-worker-accounts-in-sqlrusergroup"></a>變更中 SQLRUserGroup 的背景工作帳戶數目

如果您想要大量使用機器學習服務，您可以增加用來執行外部指令碼，如本文中所述的帳戶數目： 

+ [修改使用者帳戶集區的機器學習服務](modify-the-user-account-pool-for-sql-server-r-services.md)

根據預設，會建立 20 個帳戶，可支援 20 的並行工作階段。 平行化的工作不會耗用額外的帳戶。 例如，如果使用者執行使用平行處理的計分工作時，相同的工作帳戶中重複使用所有執行緒。