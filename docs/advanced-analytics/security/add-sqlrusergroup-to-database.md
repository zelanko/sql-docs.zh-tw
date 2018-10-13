---
title: 新增 SQLRUserGroup 作為資料庫使用者 （SQL Server 機器學習服務） |Microsoft Docs
description: 如何新增 SQLRUserGroup 作為資料庫使用者，SQL Server Machine Learning 服務。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fc5294453def64d13cc43a74a8a5fb299c3e23e3
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100319"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>新增 SQLRUserGroup 作為資料庫使用者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

建立的資料庫登入[SQLRUserGroup](../concepts/security.md#sqlrusergroup)以允許來自 R 和 Python 指令碼，目標是資料或 SQL Server 執行個體上的作業時的信任的連接。 

包含與 SQL Server 登入的連接字串或完整指定的使用者名稱和密碼的指令碼，建立登入不需要。

## <a name="when-a-login-is-required"></a>何時需要登入

如果 R 或 Python 指令碼包含連接字串，指定受信任的連線 (例如，"Trusted_Connection = True")，額外的設定是必要的使用者身分識別正確的呈現方式的 SQL Server。 外部處理序正在**SQLRUserGroup**背景工作帳戶，例如 MSSQLSERVER01，信任的使用者會以背景工作角色的身分識別。 因為此身分識別沒有 SQL Server 的登入權限，信任連接將會失敗，除非您將新增**SQLRUserGroup**當做資料庫使用者。 如需詳細資訊，請參閱 < [*隱含的驗證*](../../advanced-analytics/concepts/security.md#implied-authentication)。

恢復 Launchpad 會保留原始叫用指令碼，並執行此程序的背景工作帳戶的使用者的對應。 受信任的連線成功後的背景工作帳戶，原始的呼叫使用者的身分識別會接管，並可用來擷取資料。 您不需要將 db_datareader 權限授予**SQLRUserGroup**。

> [!Note]
>  請確定**SQLRUserGroup**有 「 允許本機登入 」 權限。 根據預設，此權限提供給所有新的本機使用者，，但在某些組織可能會強制執行更嚴格的群組原則。

## <a name="create-a-login"></a>建立登入

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，展開 [安全性] ，以滑鼠右鍵按一下 [登入] ，然後選取 [新增登入] 。

2. 在 **登入-新增**對話方塊中，選取**搜尋**。 (沒有任何項目 方塊中輸入尚未。）
    
     ![按一下 [搜尋] 以新增新的登入 machine learning](media/implied-auth-login1.png "按一下 加入新的登入 machine learning 搜尋")

3. 在 [**選取使用者或群組**方塊中，按一下**物件類型**] 按鈕。

     ![搜尋物件類型以加入新的登入 machine learning](media/implied-auth-login2.png "搜尋要加入新的登入 machine learning 的物件類型")

4. 在 **物件的型別**對話方塊中，選取**群組**。 清除所有其他核取方塊。

     ![在 [物件類型] 對話方塊中選取群組](media/implied-auth-login3.png "物件類型] 對話方塊中的 [選取群組")

4. 按一下 **進階**，確認要搜尋的位置是目前的電腦，然後按一下**立即尋找**。

     ![按一下 [立即尋找]，取得群組清單](media/implied-auth-login4.png "按一下 [立即尋找]，取得群組清單")

5. 捲動清單，直到您找到一開始在伺服器上的群組帳戶的`SQLRUserGroup`。
    
    + Launchpad 服務相關聯的群組名稱_預設執行個體_總是**SQLRUserGroup**，而不論您是否安裝了 R 或 Python 或兩者。 選取此帳戶只是預設執行個體。
    + 如果您使用_具名執行個體_，執行個體名稱會附加至的預設背景工作群組名稱， `SQLRUserGroup`。 因此，如果您的執行個體名稱為"MLTEST 」，這個執行個體的預設使用者群組名稱會是**SQLRUserGroupMLTest**。
 
     ![範例伺服器上的群組](media/implied-auth-login5.png "範例伺服器上的群組")
   
5. 按一下 **確定**以關閉 進階的搜尋 對話方塊。

    > [!IMPORTANT]
    > 請確定您已選取正確的帳戶，執行個體。 每個執行個體可以使用只有自己的 Launchpad 服務並為該服務建立的群組。 執行個體無法共用 Launchpad 服務或背景工作帳戶。

6. 按一下 [ **[確定]** 以關閉**選取使用者或群組**] 對話方塊。

7. 在 [**登入-新增**] 對話方塊中，按一下**確定**。 依預設，登入指派給 **公用** 角色，並有連接到資料庫引擎的權限。