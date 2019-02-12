---
title: 使用已註冊的伺服器執行視需要評估 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security"
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 31282041abe538bd51ba4b1367f70cd3c5fa3d5b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56030789"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>使用已註冊的伺服器執行指定評估
  您可以使用已註冊的伺服器，針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一個或多個執行個體執行最佳作法原則的指定評估。 您可以使用本機伺服器群組或中央管理伺服器。  
  
> [!NOTE]  
>  您可以針對執行 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 更新版本的伺服器群組成員執行最佳作法原則的指定評估。 不過，如果有一些 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 或 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] 中不支援之原則參考的屬性，您可能會收到例外狀況錯誤。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行這個工作，必須已經在已註冊的伺服器中設定一個或多個伺服器註冊。 如需詳細資訊，請參閱下列主題：  
  
-   [建立或編輯伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [註冊連接的伺服器&#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)。  
  
-   [建立中央管理伺服器與伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>若要針對伺服器群組評估最佳做法原則  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的 **[檢視]** 功能表中，按一下 **[已註冊的伺服器]**。  
  
2.  依序展開**Database Engine**，然後展開**本機伺服器群組**，或**中央管理伺服器**，取決於您的設定。  
  
3.  執行下列任一步驟：  
  
    -   評估原則所管理的本機伺服器群組的所有伺服器或中央管理伺服器，以滑鼠右鍵按一下 本機伺服器群組名稱或中央管理伺服器名稱，然後按一下**評估原則**.  
  
        > [!NOTE]  
        >  當您透過中央管理伺服器管理原則時，不會針對中央管理伺服器本身評估原則。  
  
    -   若要評估的原則針對特定伺服器或伺服器群組，依序展開**本機伺服器群組**或中央管理伺服器名稱，以滑鼠右鍵按一下伺服器或您想要評估原則，然後按一下 伺服器群組**評估原則**。  
  
4.  在 [**評估原則**] 對話方塊中的 [下一步**來源**方塊中，按一下省略符號 (**...**)] 按鈕。  
  
5.  在 [**選取來源**] 對話方塊中，您可以選取**檔案**或**Server**做為評估之原則檔案的來源。 如果您按一下**Server**，您可以執行任何先前已匯入至本機或遠端伺服器上的原則式管理的最佳作法原則的視需要評估。 在本教學課程中，您不需要按**檔案**，然後選取您想要評估的個別原則檔案。 若要這樣做，請遵循下列步驟：  
  
    1.  按一下 **檔案**。  
  
    2.  旁**檔案**，按一下省略符號 (**...**) 按鈕。  
  
    3.  選取一或多個.xml 原則檔案來評估，然後按一下**開啟**。  
  
         選取的檔案清單會出現在**檔案** 方塊中。  
  
    4.  在 [**選取來源**] 對話方塊中，按一下**確定**。  
  
    5.  如果**正在載入原則** 對話方塊出現時，按一下**關閉**。  
  
     您選取的原則會列在**原則選取**頁面。 請注意，原則旁邊的警告圖示表示該原則包含指令碼。  
  
6.  按一下  **Evaluate**來評估原則。  
  
7.  對於某些原則失敗，以原則為基礎的管理可讓您立即強制符合目標上的原則。 若是此類失敗，失敗的原則旁邊會出現一個核取方塊。 如果您選取核取方塊，或按一下失敗的原則使用的資料列，核取方塊會出現在**目標詳細資料**評估失敗的目標執行個體旁邊的窗格。 若有選取任何核取方塊，**套用**按鈕會變成可用。 當您按一下 **套用**，不符合規範的設定將會自動更新您選取的目標執行個體上。  
  
    > [!CAUTION]  
    >  請在自動更新目標執行個體之前，確認您完全了解原則設定。 我們建議您選取一或多個核取方塊之後，您按一下**指令碼**，然後選擇 輸出位置，讓您可以檢閱基礎[!INCLUDE[tsql](../includes/tsql-md.md)]程式碼之前套用所做的變更。  
  
8.  若要檢視之原則的詳細的結果，請按一下 中的原則**結果**資料表。 **目標詳細資料**表顯示每個執行個體的詳細資料。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：評估最佳做法原則根據排程](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>另請參閱  
 [監視和強制最佳做法，使用原則式管理](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [使用中央管理伺服器管理多部伺服器](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
