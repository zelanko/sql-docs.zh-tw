---
title: 將排程的原則部署至多個實例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: f551b8e8-3668-4ed4-852f-bae826254f4f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0d3f2412114e50292c91908b3a20c433d022b239
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057608"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>將已排程的原則部署至多個執行個體
  您可以使用已註冊的伺服器，將已排程的原則從中央位置部署到 Managed 伺服器。 您可以從本機伺服器群組，或從中央管理伺服器部署已排程的原則。  
  
 在這個工作中，您將進行下列作業：  
  
1.  將您在先前工作中排程的原則匯出至資料夾。  
  
2.  將已排程的原則部署到透過已註冊的伺服器所管理的目標執行個體。  
  
 您必須在已完成本課程先前工作的電腦上執行這些工作。  
  
## <a name="prerequisites"></a>Prerequisites  
 此工作的必要條件如下：  
  
-   您必須先完成本課程先前的工作。  
  
-   其上要部署已排程原則的執行個體必須是執行 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或更新版本。 若要進行自動化作業，原則必須儲存在本機位置，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 版本不支援此功能。  
  
-   您要部署已排程原則的伺服器，必須在 [**本機伺服器群組**] 或 [**中央管理伺服器**] 節點的 [已註冊的伺服器] 中註冊。 如需詳細資訊，請參閱下列主題：  
  
    -   [建立或編輯伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [&#40;SQL Server Management Studio&#41;註冊已連線的伺服器](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)。  
  
    -   [建立中央管理伺服器與伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>若要將已排程的原則匯出為 .xml 檔案  
  
1.  在您在上一個工作中設定排程原則的伺服器上，依序展開 [**管理**]、[**原則管理**] 和 [**原則**]。  
  
2.  在 [檢視]**** 功能表上，按一下 [物件總管詳細資料]****。  
  
3.  在 [**物件總管詳細資料**] 窗格中，選取您想要透過 [已註冊的伺服器] 部署到其他伺服器的所有已排程最佳做法原則。  
  
    > [!NOTE]  
    >  您可以按一下 [**類別**] 標題，依類別目錄來排序原則。  
  
4.  以滑鼠右鍵按一下選取專案，然後按一下 [**匯出原則**]。  
  
5.  如果您選取了多個要匯出的原則，請在 [**流覽資料夾**] 對話方塊中，選取目的地資料夾，或建立新的資料夾。 在此課程中，請建立路徑為**c：\ Scheduled_BP_Policies**的新資料夾，然後按一下 **[確定]**。  
  
     如果您只選取一個要匯出的原則，請在 [**匯出原則**] 對話方塊中，建立路徑為**c：\ Scheduled_BP_Policies**的新資料夾，按一下 [**開啟**]，然後按一下 [**儲存**]。  
  
     .xml 原則檔案是建立在資料夾位置。  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>若要將已排程的原則部署到透過已註冊的伺服器所管理的伺服器  
  
1.  在 [檢視]**** 功能表上，按一下 [已註冊的伺服器]****。  
  
2.  依序展開 [**資料庫引擎**]、[**本機伺服器群組**] 或 [**中央管理伺服器**]，以滑鼠右鍵按一下您要部署原則的節點，然後按一下 [匯**入原則**]。  
  
    > [!NOTE]  
    >  如果您以滑鼠右鍵按一下 [**本機伺服器群組**] 或 [中央管理伺服器本身]，原則就會部署到所有受管理的伺服器。 如果以滑鼠右鍵按一下特定的伺服器群組，原則就只會部署到該群組中的伺服器。 如果以滑鼠右鍵按一下特定的已註冊伺服器，原則就只會部署到該伺服器。  
  
3.  在 [**要匯入**的檔案] 旁，按一下省略號按鈕（**...**）。  
  
4.  在 [**選取原則**] 對話方塊中，流覽至您儲存已排程原則的資料夾位置。 在此範例中，流覽至位置**c：\ Scheduled_BP_Policies**。  
  
5.  選取您要匯入目標實例的原則，然後按一下 [**開啟**]。  
  
6.  在 [匯**入**] 對話方塊的 [**原則狀態**] 清單中，選取所需的原則狀態。 您可以選擇在匯入原則保留原則狀態 (啟用) 或加以停用。 請注意，原則必須啟用才能按排程執行。  
  
7.  按一下 **[確定]** ，將原則匯入至所有目標實例。  
  
    > [!NOTE]  
    >  如果發生任何錯誤，[匯**入**] 對話方塊就不會消失。 按一下 [**記錄**] 頁面來檢查訊息。 按一下 [**取消**] 關閉對話方塊。  
  
8.  若要從目標實例中查看原則，請連接到實例，開啟物件總管，展開 [**管理**]，然後展開 [**原則**]。 您應該會在 [**原則**] 節點中看到匯入的原則。 您可以在每個原則上按兩下來檢視排程或變更設定。  
  
    > [!NOTE]  
    >  若要在已排程的原則執行後檢視評估結果，請開啟目標執行個體上的「原則記錄」記錄檔。 若要開啟記錄檔，請以滑鼠右鍵按一下 [**原則管理**]，然後按一下 [**查看歷程記錄**]。  
  
## <a name="summary"></a>摘要  
 本教學課程已為您示範如何針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一個或多個執行個體，視需要或按排程來執行最佳做法原則的評估。  
  
## <a name="next"></a>下一個  
 本教學課程已完成。 若要回到開頭，請參閱[教學課程：使用以原則為基礎的管理來評估最佳作法](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md)。  
  
 若要查看教學課程的清單 [!INCLUDE[ssDE](../includes/ssde-md.md)] ，請按一下 [[資料庫引擎教學](../relational-databases/database-engine-tutorials.md)課程]。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
