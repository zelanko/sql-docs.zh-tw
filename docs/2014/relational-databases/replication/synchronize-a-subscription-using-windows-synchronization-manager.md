---
title: 同步處理訂用帳戶使用 Windows Synchronization Manager (Windows Synchronization Manager) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], Windows Synchronization Manager
- Windows Synchronization Manager
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d12b1cc5b4626ab9093639d69a7ee724f2cc745d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147428"
---
# <a name="synchronize-a-subscription-using-windows-synchronization-manager-windows-synchronization-manager"></a>使用 Windows Synchronization Manager 同步處理訂閱 (Windows Synchronization Manager)
  如果 Microsoft[!INCLUDE[msCoName](../../includes/msconame-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows Synchronization Manager 在相同的電腦上執行，則 Synchronization Manager 只能用於同步處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的訂閱 (它也可以用於同步處理離線檔案和網頁)。 若要使用 Synchronization Manager：  
  
1.  在 [訂閱屬性 - \<訂閱者>: \<訂閱資料庫>] 對話方塊中，啟用同步處理提取訂閱與 Windows Synchronization Manager。 如需存取此對話方塊的詳細資訊，請參閱[檢視及修改提取訂閱屬性](view-and-modify-pull-subscription-properties.md)。  
  
2.  透過 Windows 中的 **[開始]** 功能表存取 Synchronization Manager。  
  
 Synchronization Manager 允許您為合併訂閱使用「互動解決器」。 通常，同步處理期間偵測到的衝突會自動解決，但是如果啟用了互動式解決方案，衝突可由使用者在同步處理期間解決。 如果是在 Windows Synchronization Manager 之外執行同步處理 (如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或複寫監視器中已排程的同步處理或視需要同步處理)，則不需要使用者的介入，就會根據為發行項指定的解決器自動解決衝突。  
  
> [!NOTE]  
>  從 [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 和 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]開始，64 位元版本的 Windows Synchronization Manager 無法偵測 32 位元訂閱。  
  
### <a name="to-enable-the-synchronization-of-pull-subscriptions-with-windows-synchronization-manager"></a>若要使用 Windows Synchronization Manager 啟用提取訂閱同步處理  
  
1.  在 [訂閱屬性 - \<訂閱者>: \<訂閱資料庫>] 對話方塊的 [一般] 頁面中，針對 [使用 Windows Synchronization Manager] 選項選取 [啟用]。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-synchronize-a-pull-subscription-with-synchronization-manager"></a>若要使用 Synchronization Manager 同步處理提取訂閱  
  
1.  請利用下列其中一種方法來啟動 Synchronization Manager：  
  
    -   在 Internet Explorer 中，按一下 **[工具]**，然後按一下 **[同步處理]**。  
  
    -   按一下 **[開始]**，依序指向 **[程式集]** (或 **[程式集]**) 和 **[附屬應用程式]**，然後按一下 **[同步處理]**。  
  
    -   按一下 **[開始]**，然後按一下 **[執行]** 在 [**執行**] 對話方塊中，輸入`mobsync.exe`中**開啟**欄位，，然後按一下 **[確定]**。  
  
2.  在 **[要同步處理的項目]** 對話方塊中，選取要同步處理的訂閱。 訂閱會列在電腦上安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之下。  
  
3.  按一下 **[同步處理]**。  
  
### <a name="to-reinitialize-a-pull-subscription-with-synchronization-manager"></a>若要使用 Synchronization Manager 重新初始化提取訂閱  
  
1.  在 **[要同步處理的項目]** 對話方塊中，選取訂閱，然後按一下 **[屬性]**。  
  
2.  在 **[SQL Server 訂閱屬性]** 對話方塊中，按一下 **[重新初始化訂閱]**。  
  
3.  按一下 **[是]**。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     下次同步處理訂閱時，依預設，訂閱資料庫會套用一個新的快照集。 如需詳細資訊，請參閱 [重新初始化訂閱](reinitialize-subscriptions.md)。  
  
> [!NOTE]  
>  合併式複寫允許在套用快照集前，將尚未處理完畢的變更上傳到「發行者」，但是此選項在 Synchronization Manager 中不可用。 若要上傳變更，請在重新初始化訂閱前，對其執行同步處理。  
  
### <a name="to-set-properties-for-a-pull-subscription-in-synchronization-manager"></a>若要在 Synchronization Manager 中設定提取訂閱的屬性  
  
1.  在 **[要同步處理的項目]** 對話方塊中，選取訂閱，然後按一下 **[屬性]**。  
  
2.  在下列索引標籤中檢視並修改屬性：  
  
    -   **識別**  
  
    -   **[訂閱者登入]**、 **[散發者登入]** 和 **[發行者登入]** (僅用於合併式複寫)  
  
    -   **[Web 伺服器資訊]** (用於執行 SQL Server 2005 或更新版本之「訂閱者」端的合併訂閱)  
  
    -   **其他**  
  
     建議對所有連接使用「Windows 驗證」。 如需「散發代理程式」和「合併代理程式」所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](security/replication-agent-security-model.md)＞。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-pull-subscription-from-synchronization-manager"></a>若要從 Synchronization Manager 中移除提取訂閱  
  
1.  在 **[要同步處理的項目]** 對話方塊中，選取訂閱，然後按一下 **[屬性]**。  
  
2.  在 **[SQL Server 訂閱屬性]** 對話方塊中按一下 **[移除訂閱]**。  
  
3.  在 **[移除訂閱]** 對話方塊中選取一個選項。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-interactive-resolver"></a>若要使用互動解決器  
  
1.  啟用發行項和訂閱以使用互動式解決方案。 如需詳細資訊，請參閱[指定合併發行項的互動式衝突解決方法](publish/specify-interactive-conflict-resolution-for-merge-articles.md)。  
  
2.  在 Synchronization Manager 中開始同步處理訂閱之後，如果啟用了互動式衝突解決方案，且一個或多個發行項有衝突，則「互動解決器」會自動啟動。 「互動解決器」每次顯示一個衝突，並為每個衝突提供一個建議的解決方案 (視建立發行集和訂閱時指定的解決器而定)。  
  
3.  選擇性地編輯任何在「互動解決器」中顯示的資料行，然後按下列其中一個按鈕，以解決衝突：  
  
    -   **[接受建議]**  
  
    -   **[接受發行者]**  
  
    -   **[接受訂閱者]**  
  
    -   **[自動解決所有衝突]** (會解決目前所有的衝突，而無需進一步的輸入)  
  
     選取的資料列然後會被套用到「發行者」和 (或)「訂閱者」；在後續同步處理期間，它會傳播到其他節點。  
  
> [!NOTE]  
>  僅當編輯為針對解決方案所選取之資料列的一部分時，才會被套用。 例如，如果您在 **[發行者]** 下進行了編輯，然後按一下 **[接受訂閱者]**，則編輯會被捨棄。  
  
## <a name="see-also"></a>另請參閱  
 [互動式衝突解決方法](merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
  
