---
title: 為 SQLRUserGroup 建立登入
description: 針對使用隱含驗證的回送連線, 請在 SQL Server 中建立登入以進行 SQLRUserGroup, 讓背景工作帳戶可以登入伺服器, 以將身分識別轉換回呼叫的使用者。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 74330d37a037b0951c4964cafbd6e0c26b4fdea1
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345635"
---
# <a name="create-a-login-for-sqlrusergroup"></a>為 SQLRUserGroup 建立登入
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

當腳本中的「迴圈執行」[連接](../../advanced-analytics/concepts/security.md#implied-authentication)指定*信任連接*, 而用來執行物件的身分識別是 Windows 使用者帳戶時, 請在[SQLRUserGroup](../concepts/security.md#sqlrusergroup)的[SQL Server 中建立登入](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login)。

信任的連線是`Trusted_Connection=True`在連接字串中的連接。 當 SQL Server 收到指定信任連接的要求時, 它會檢查目前 Windows 使用者的身分識別是否有登入。 針對以背景工作帳戶執行的外部進程 (例如從**SQLRUSERGROUP**MSSQLSERVER01), 要求會失敗, 因為這些帳戶預設沒有登入。

您可以藉由建立**SQLServerRUserGroup**的登入來解決連接錯誤。 如需有關身分識別和外部進程的詳細資訊, 請參閱擴充性[架構的安全性總覽](../concepts/security.md)。

> [!Note]
> 請確定**SQLRUserGroup**具有「允許本機登入」許可權。 根據預設, 此許可權會提供給所有新的本機使用者, 但某些組織更嚴格的群組原則可能會停用此許可權。

## <a name="create-a-login"></a>建立登入

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，展開 [安全性]  ，以滑鼠右鍵按一下 [登入]  ，然後選取 [新增登入]  。

2. 在 [**登入-新增**] 對話方塊中, 選取 [**搜尋**]。 (還不要在方塊中輸入任何內容)。
    
     ![按一下 [搜尋], 為機器學習服務新增新的登]入(media/implied-auth-login1.png "按一下 [搜尋], 為機器學習服務新增新的登")入

3. 在 [**選取使用者或群組**] 方塊中, 按一下 [**物件類型**] 按鈕。

     ![搜尋物件類型以新增機器學習服務的登]入(media/implied-auth-login2.png "搜尋物件類型以新增機器學習服務的登")入

4. 在 [**物件類型**] 對話方塊中, 選取 [**群組**]。 清除所有其他核取方塊。

     ![選取物件類型中的群組對話方塊](media/implied-auth-login3.png "選取物件類型中的群組對話方塊")

4. 按一下 [ **Advanced**], 確認要搜尋的位置是目前的電腦, 然後按一下 [**立即尋找**]。

     ![按一下 [立即尋找] 以取得群組清單](media/implied-auth-login4.png "按一下 [立即尋找] 以取得群組清單")

5. 流覽伺服器上的群組帳戶清單, 直到您找到一開始`SQLRUserGroup`為止。
    
    + 與_預設實例_的啟動列服務相關聯的組名一律是**SQLRUserGroup**, 不論您是否已安裝 R 或 Python 或兩者。 僅針對預設實例選取此帳戶。
    + 如果您使用的是_已命名的實例_, 實例名稱會附加至預設背景工作組名`SQLRUserGroup`的名稱。 例如, 如果您的實例名稱為 "MLTEST", 這個實例的預設使用者組名會是**SQLRUserGroupMLTest**。
 
    ![伺服器上的群組範例](media/implied-auth-login5.png "伺服器上的群組範例")
   
5. 按一下 **[確定]** 以關閉 [高級搜尋] 對話方塊。

    > [!IMPORTANT]
    > 請確定您已為實例選取正確的帳戶。 每個實例只能使用它自己的啟動列服務, 以及為該服務建立的群組。 實例無法共用啟動列服務或背景工作帳戶。

6. 再按一次 **[確定]** , 關閉 [**選取使用者或群組**] 對話方塊。

7. 在 [**登入-新增**] 對話方塊中, 按一下 **[確定]** 。 依預設，登入指派給 **公用** 角色，並有連接到資料庫引擎的權限。

## <a name="next-steps"></a>後續步驟

+ [安全性概觀](../concepts/security.md)
+ [擴充性架構](../concepts/extensibility-framework.md)
