---
title: 在 Active Directory 模式中部署 - 先決條件
titleSuffix: SQL Server Big Data Cluster
description: 設定適用於 SQL Server 巨量資料叢集的 Active Directory
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c25038680d71257e609d99460841d63b8e87d33
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898665"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode-prerequisites"></a>在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]：先決條件

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文件說明如何準備在 Active Directory 驗證模式中部署 SQL Server 巨量資料叢集 (BDC)。 叢集會使用現有的 AD 網域進行驗證。

>[!Note]
>在 SQL Server 2019 CU5 版本之前，巨量資料叢集中有一項限制，使您只能針對一個 Active Directory 網域部署一個叢集。 CU5 版本中已移除這項限制，請參閱[概念：在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deployment-background.md)，以取得新功能的詳細資料。 本文中的範例已經過調整，同時適用於兩種部署使用案例。

## <a name="background"></a>背景

若要啟用 Active Directory (AD) 驗證，BDC 會自動建立叢集中各種服務所需的使用者、群組、機器帳戶和服務主體名稱 (SPN)。 若要提供這些帳戶的一些內含項目，並允許範圍權限，我們建議在進行叢集部署之前先建立組織單位 (OU)。 將會在在部署期間建立所有 BDC 相關 AD 物件。 

## <a name="pre-requisites"></a>必要條件

### <a name="organizational-unit-ou"></a>組織單位 (OU)
組織單位 (OU) 是 Active Directory 內的子分支，其中會放置使用者、群組，甚至是其他組織單位。 大型圖片組織單位可以用來鏡像組織的功能或商業結構。 在此文章文中，我們將建立名為 `bdc` 的 OU 作為範例。 

>[!NOTE]
>組織單位 (OU) 代表系統管理界限，並可讓客戶控制資料管理員的授權範圍。 

您可以依照 [OU 設計原則](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts)決定在組織內使用 OU 的最佳結構。

### <a name="ad-account-for-bdc-domain-service-account"></a>BDC 網域服務帳戶的 AD 帳戶

若要能夠自動在 Active Directory 中建立所有必要物件，BDC 需要一個擁有特殊權限、可在所提供組織單位 (OU) 內建立使用者、群組與電腦帳戶的 AD 帳戶。 此文章將說明如何設定此 AD 帳戶的權限。 我們使用 AD 帳戶呼叫 `bdcDSA` 作為此文章中的範例。

### <a name="auto-generated-active-directory-objects"></a>已自動產生 Active Directory 物件
BDC 部署會自動產生帳戶與群組名稱。 每個帳戶都代表 BDC 中的服務，而且會在 BDC 叢集使用中的整個存留期中受 BDC 管理。 那些帳戶擁有每個服務所需的服務主體名稱 (SPN)。  如需其所管理 AD 自動產生的帳戶、群組與服務的完整清單，請參閱[自動產生的 Active Directory 物件](active-directory-objects.md)。

>[!IMPORTANT]
>視網域控制站中設定的密碼到期原則而定，這些帳戶的密碼可能會過期。 預設的到期原則為 42 天。 沒有任何機制可輪替 BDC 中所有帳戶的認證，因此一旦符合到期期限，叢集將會變成無法運作。 為因應此問題，請在網域控制站中將 BDC 服務帳戶的到期原則更新為 [密碼永久有效]。 此動作可以在到期時間之前或之後完成。 如果是後者，Active Directory 將會重新啟用過期的密碼。
>
>下圖顯示在 Active Directory [使用者和電腦] 中設定此屬性的位置。
>
>:::image type="content" source="media/deploy-active-directory/image25.png" alt-text="設定密碼到期原則":::

以下步驟假設您已經有 Active Directory 網域控制站。 如果您沒有網域控制站，下列[指南](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) \(英文\) 包含的步驟可能有幫助。

## <a name="create-ad-objects"></a>建立 AD 物件

使用 AD 整合部署 BDC 之前，請執行下列事項：

1. 建立將會儲存所有 BDC 相關 AD 物件的組織單位 (OU)。 或者，您也可以在部署時選擇現有的 OU。
1. 為 BDC 建立 AD 帳戶，或使用現有帳戶，並提供所提供組織單位 (OU) 內的正確權限給此 BDC AD 帳戶。

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>為 BDC 網域服務帳戶在 AD 中建立使用者

巨量資料叢集需要具有特定權限的帳戶。 在繼續之前，請確定您已有現有 AD 帳戶，或建立一個新帳戶，讓巨量資料叢集能夠用來設定必要物件。

若要在 AD 中建立新使用者，您可以在網域或 OU 上按一下滑鼠右鍵，然後選取 [新增] > [使用者]：

![Active Directory 使用者對話方塊](./media/deploy-active-directory/image12.png)

在本文中，將稱呼此使用者「BDC 網域服務帳戶」。

### <a name="create-an-ou"></a>建立 OU

在網域控制站上，開啟 [Active Directory 使用者及電腦]。 在左側面板上，以滑鼠右鍵按一下想要在其下建立 OU 的目錄，然後選取 [新增] \> [組織單位]，然後遵循精靈的提示來建立 OU。 或者，您可以使用 PowerShell 建立 OU：

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

本文中的範例使用 `bdc` 作為 OU 名稱。

![Active Directory 組織單位](./media/deploy-active-directory/image13.png)

![新增物件 - 組織單位](./media/deploy-active-directory/image14.png)

### <a name="set-permissions-for-an-ad-account"></a>設定 AD 帳戶的權限

不論您已經建立新 AD 使用者，或使用現有 AD 使用者，該使用者都需要有特定權限。 當 BDC 控制器將叢集加入 AD 時，將會使用此使用者帳戶。

BDC 網域服務帳戶 (DSA) 必須能在 OU 中建立使用者、群組和電腦帳戶。 在下列步驟中，我們已經將 BDC 網域服務帳戶命名為 `bdcDSA`。 您可以為此帳戶選擇任何名稱。

1. 在網域控制站上，開啟 [Active Directory 使用者及電腦]

1. 在左面板中，瀏覽到您的網域，再到 `bdc` 要使用的 OU

1. 以滑鼠右鍵按一下 OU，然後選取 [屬性]。

1. 移至 [安全性] 索引標籤 (請務必藉由在 OU 上按一下滑鼠右並選取 [進階功能]，再選取 [檢視])

    ![BDC 物件屬性](./media/deploy-active-directory/image15.png)

1. 按一下 [新增...] 並新增 **bdcDSA** 使用者

    ![新增 BDC 物件屬性](./media/deploy-active-directory/image16.png)

    ![選取物件](./media/deploy-active-directory/image17.png)

1. 選取 **bdcDSA** 使用者並清除所有權限，然後按一下 [進階]

1. 按一下 [新增]

    ![按一下 [新增]](./media/deploy-active-directory/image18.png)

    - 按一下 [選取主體]、插入 **bdcDSA**，然後按一下 [確定]

    - 將 [類型] 設定為 [允許]

    - 將 [套用至] 設定為 [此物件及所有子系物件]

        ![設定允許屬性](./media/deploy-active-directory/image19.png)

    - 向下捲動到底部，然後按一下 [全部清除]

    - 捲動回頂端，然後選取：
       - **讀取全部內容**
       - **寫入全部內容**
       - **建立電腦物件**
       - **刪除電腦物件**
       - **建立群組物件**
       - **刪除群組物件**
       - **建立使用者物件**
       - **刪除使用者物件**

    - 按一下 [檔案] &gt; [新增] &gt; [專案] 

- 按一下 [新增]

    - 按一下 [選取主體]、插入 **bdcDSA**，然後按一下 [確定]

    - 將 [類型] 設定為 [允許]

    - 將 [套用至] 設定為 [子系電腦物件]

    - 向下捲動到底部，然後按一下 [全部清除]

    - 捲動回頂端，然後選取 [重設密碼]

    - 按一下 [檔案] &gt; [新增] &gt; [專案] 

- 按一下 [新增]

    - 按一下 [選取主體]、插入 **bdcDSA**，然後按一下 [確定]

    - 將 [類型] 設定為 [允許]

    - 將 [套用至] 設定為 [子系使用者物件]

    - 向下捲動到底部，然後按一下 [全部清除]

    - 捲動回頂端，然後選取 [重設密碼]

    - 按一下 [檔案] &gt; [新增] &gt; [專案] 

- 再按兩次 [確定]，關閉開啟的對話方塊

## <a name="next-steps"></a>後續步驟

[在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deploy.md)

[針對 SQL Server 巨量資料叢集 Active Directory 整合進行疑難排解](troubleshoot-active-directory.md)

[概念：在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deployment-background.md)
