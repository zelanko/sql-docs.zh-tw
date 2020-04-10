---
title: 為 SQLRUserGroup 建立登入
description: 針對使用隱含驗證的回送連線，請在 SQL Server 中建立 SQLRUserGroup 的登入，讓背景工作帳戶可以登入伺服器，以便將身分識別轉換回呼叫的使用者。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c57a62e954ae8cb0fc52c9a5ead22d418243c0b8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117121"
---
# <a name="create-a-login-for-sqlrusergroup"></a>為 SQLRUserGroup 建立登入
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

當指令碼中的[回送連線](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login)指定[信任連線](../concepts/security.md#sqlrusergroup)，而且用來執行包含程式碼之物件的身分識別是 Windows 使用者帳戶時，為 [SQLRUserGroup](../../machine-learning/concepts/security.md#implied-authentication) 建立 *SQL Server 中的登入*。

信任連線是在連接字串中有 `Trusted_Connection=True` 的連線。 當 SQL Server 收到指定信任連線的要求時，它會檢查目前 Windows 使用者的身分識別是否有登入。 對於以背景工作帳戶執行的外部處理序 (例如來自 **SQLRUserGroup** 的 MSSQLSERVER01)，要求會失敗，因為這些帳戶預設沒有登入。

您可以建立 **SQLServerRUserGroup** 的登入，以解決連線錯誤的問題。 如需有關身分識別和外部處理序的詳細資訊，請參閱[擴充性架構的安全性概觀](../concepts/security.md)。

> [!Note]
> 請確定 **SQLRUserGroup** 擁有「允許本機登入」權限。 根據預設，此權限會提供給所有新的本機使用者，但某些組織較嚴格的群組原則可能會停用此權限。

## <a name="create-a-login"></a>建立登入

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [物件總管] 中，展開 [安全性]  ，以滑鼠右鍵按一下 [登入]  ，然後選取 [新增登入]  。

2. 在 [登入 - 新增]  對話方塊中，選取 [搜尋]  (還不要在方塊中輸入任何內容)。
    
     ![按一下 [搜尋] 來為機器學習新增登入](media/implied-auth-login1.png "按一下 [搜尋] 來為機器學習新增登入")

3. 在 [選取使用者或群組]  方塊中，按一下 [物件類型]  按鈕。

     ![搜尋 [物件類型] 來為機器學習新增登入](media/implied-auth-login2.png "搜尋 [物件類型] 來為機器學習新增登入")

4. 在 [物件類型]  對話方塊中，選取 [群組]  。 清除其他所有的核取方塊。

     ![選取 [物件類型] 對話方塊中的 [群組]](media/implied-auth-login3.png "選取 [物件類型] 對話方塊中的 [群組]")

4. 按一下 [進階]  ，確認要搜尋的位置是目前的電腦，然後按一下 [立即尋找]  。

     ![按一下 [立即尋找] 來取得群組清單](media/implied-auth-login4.png "按一下 [立即尋找] 來取得群組清單")

5. 瀏覽伺服器上的群組帳戶清單，直到您找到一個開頭為 `SQLRUserGroup` 的清單為止。
    
    + 不論您安裝的是 R、Python 還是兩者，與_預設執行個體_的啟動控制板服務相關聯之群組的名稱一律是 **SQLRUserGroup**。 僅針對預設執行個體選取此帳戶。
    + 如果您使用的是_具名執行個體_，執行個體名稱會附加至預設背景工作群組名稱 `SQLRUserGroup` 的名稱。 例如，如果您的執行個體名稱為 "MLTEST"，則此執行個體的預設使用者群組名稱會是 **SQLRUserGroupMLTest**。
 
    ![伺服器上群組的範例](media/implied-auth-login5.png "伺服器上群組的範例")
   
5. 按一下 [確定]  以關閉 [進階搜尋] 對話方塊。

    > [!IMPORTANT]
    > 請確定您已為執行個體選取正確的帳戶。 每個執行個體都只能使用自己的啟動控制板服務，以及為該服務建立的群組。 執行個體無法共用啟動控制板服務或背景工作帳戶。

6. 再按一下 [確定]  ，關閉 [選取使用者或群組]  對話方塊。

7. 在 [登入 - 新增]  對話方塊中，按一下 [確定]  。 依預設，登入指派給 **公用** 角色，並有連接到資料庫引擎的權限。

## <a name="next-steps"></a>後續步驟

+ [安全性概觀](../concepts/security.md)
+ [擴充性架構](../concepts/extensibility-framework.md)
