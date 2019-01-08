---
title: 新增 SQLRUserGroup 作為資料庫使用者-SQL Server Machine Learning 服務
description: 對於使用隱含的驗證的回送連線，新增 SQLRUserGroup 作為資料庫使用者，使背景工作帳戶可以登入伺服器上，以傳回給呼叫使用者的身分識別轉換。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: abd0745126a4f2a23cf559500b93d2fa53fa2cf9
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432351"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>新增 SQLRUserGroup 作為資料庫使用者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

建立的資料庫登入[SQLRUserGroup](../concepts/security.md#sqlrusergroup)當[循迴路連線](../../advanced-analytics/concepts/security.md#implied-authentication)指令碼中指定*信任連接*，以及用來執行物件的識別包含您的程式碼是 Windows 使用者帳戶。

受信任的連接是指`Trusted_Connection=True`連接字串中。 當 SQL Server 收到要求，指定受信任的連線時，它會檢查目前的 Windows 使用者的身分識別是否有登入。 執行為背景工作帳戶的外部處理序 (例如 MSSQLSERVER01 從**SQLRUserGroup**)，則要求會失敗，因為這些帳戶依預設沒有登入。

您可以藉由提供解決連線錯誤**SQLServerRUserGroup**的 SQL Server 登入。 如需身分識別和外部處理序的詳細資訊，請參閱[擴充性架構的安全性概觀](../concepts/security.md)。

> [!Note]
>  請確定**SQLRUserGroup**有 「 允許本機登入 」 權限。 根據預設，此權限提供給所有新的本機使用者，但在某些組織中更嚴格的群組原則可能會停用此權限。

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
    + 如果您使用_具名執行個體_，執行個體名稱會附加至的預設背景工作群組名稱， `SQLRUserGroup`。 例如，如果您的執行個體名稱為"MLTEST 」，這個執行個體的預設使用者群組名稱會是**SQLRUserGroupMLTest**。
 
 ![範例伺服器上的群組](media/implied-auth-login5.png "範例伺服器上的群組")
   
5. 按一下 **確定**以關閉 進階的搜尋 對話方塊。

    > [!IMPORTANT]
    > 請確定您已選取正確的帳戶，執行個體。 每個執行個體可以使用只有自己的 Launchpad 服務並為該服務建立的群組。 執行個體無法共用 Launchpad 服務或背景工作帳戶。

6. 按一下 [ **[確定]** 以關閉**選取使用者或群組**] 對話方塊。

7. 在 [**登入-新增**] 對話方塊中，按一下**確定**。 依預設，登入指派給 **公用** 角色，並有連接到資料庫引擎的權限。

## <a name="next-steps"></a>後續步驟

+ [安全性概觀](../concepts/security.md)
+ [擴充性架構](../concepts/extensibility-framework.md)