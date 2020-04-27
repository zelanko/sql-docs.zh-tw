---
title: 使用已註冊的伺服器來執行隨選評估 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a3a79a6ec655e91264d6fcc00db5a920ad82a21e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66822378"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>使用已註冊的伺服器執行指定評估

  您可以使用已註冊的伺服器，針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一個或多個執行個體執行最佳作法原則的指定評估。 您可以使用本機伺服器群組或中央管理伺服器。  
  
> [!NOTE]  
>  您可以針對執行 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 更新版本的伺服器群組成員執行最佳作法原則的指定評估。 不過，如果有一些 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 或 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)] 中不支援之原則參考的屬性，您可能會收到例外狀況錯誤。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行這個工作，必須已經在已註冊的伺服器中設定一個或多個伺服器註冊。 如需詳細資訊，請參閱下列主題：  
  
-   [建立或編輯伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [&#40;SQL Server Management Studio&#41;註冊已連線的伺服器](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)。  
  
-   [建立中央管理伺服器與伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>若要針對伺服器群組評估最佳做法原則  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的 **[檢視]** 功能表中，按一下 **[已註冊的伺服器]**。  
  
2.  展開 [**資料庫引擎**]，然後展開 [**本機伺服器群組**] 或 [**中央管理伺服器**]，視您的設定而定。  
  
3.  執行下列任一步驟：  
  
    -   若要針對本機伺服器群組或中央管理伺服器所管理的所有伺服器來評估原則，請以滑鼠右鍵按一下本機伺服器組名或中央管理伺服器名稱，然後按一下 [**評估原則**]。  
  
        > [!NOTE]  
        >  當您透過中央管理伺服器管理原則時，不會針對中央管理伺服器本身評估原則。  
  
    -   若要針對特定伺服器或伺服器群組評估原則，請展開 [**本機伺服器群組**] 或 [中央管理伺服器名稱]，以滑鼠右鍵按一下您想要評估原則的伺服器或伺服器群組，然後按一下 [**評估原則**]。  
  
4.  在 [**評估原則**] 對話方塊中，按一下 [**來源**] 方塊旁的省略號（**...**）按鈕。  
  
5.  在 [**選取來源**] 對話方塊中，您可以選取 [檔案 **] 或 [** **伺服器**] 做為要評估之原則檔案的來源。 如果您按一下 [**伺服器**]，可以針對先前匯入本機或遠端伺服器上以原則為基礎之管理的任何最佳作法原則，執行視需要評估。 在本教學課程**中，您將按一下 [** 檔案]，然後選取您想要評估的個別原則檔案。 若要這樣做，請執行下列步驟：  
  
    1.  按一下 **[** 檔案]。  
  
    2.  在 [檔案]**旁，按一下**省略號（**...**）按鈕。  
  
    3.  選取一或多個要評估的 .xml 原則檔案，然後按一下 [**開啟**]。  
  
         選取的檔案清單會出現**在 [檔案**] 方塊中。  
  
    4.  在 [**選取來源**] 對話方塊中，按一下 **[確定]**。  
  
    5.  如果出現 [**正在載入原則**] 對話方塊，請按一下 [**關閉**]。  
  
     您選取的原則會列在 [**原則選取**] 頁面上。 請注意，原則旁邊的警告圖示表示該原則包含指令碼。  
  
6.  按一下 [**評估**] 以評估原則。  
  
7.  對於某些原則失敗，以原則為基礎的管理可讓您立即強制符合目標上的原則。 若是此類失敗，失敗的原則旁邊會出現一個核取方塊。 如果您選取此核取方塊，或按一下具有失敗原則的資料列，核取方塊就會出現在評估失敗的目標實例旁的 [**目標詳細資料**] 窗格中。 如果選取了任何核取方塊，[套用]**按鈕就**會變成可用。 當**您按一下 [** 套用] 時，將會在您選取的目標實例上自動更新不符合規範的設定。  
  
    > [!CAUTION]  
    >  請在自動更新目標執行個體之前，確認您完全了解原則設定。 我們建議您在選取一個或多個核取方塊後，按一下 [**腳本**]，然後選擇輸出位置，以便您可以在套用[!INCLUDE[tsql](../includes/tsql-md.md)]變更之前，先檢查基礎程式碼。  
  
8.  若要查看原則的詳細結果，請按一下 [**結果**] 資料表中的原則。 [**目標詳細資料**] 資料表會顯示每個實例的詳細資料。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：根據排程評估最佳做法原則](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用以原則為基礎的管理來監視和強制執行最佳作法](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [使用中央管理伺服器管理多部伺服器](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
