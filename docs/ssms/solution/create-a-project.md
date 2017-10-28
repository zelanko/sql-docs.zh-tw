---
title: "建立專案 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.newproject
- vs.addnewproject
helpviewer_keywords:
- projects [SQL Server Management Studio], creating
ms.assetid: 7897be19-365b-4b06-bcf0-8a669f67a673
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 07eabcd5f183ff5ecba9d6718a8a51aae8a80503
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-project"></a>建立專案
您可以在現有方案內，建立一或多個專案。  
  
### <a name="to-create-a-new-project-and-add-it-to-a-solution"></a>建立新的專案，將它加入方案中  
  
1.  在 [方案總管] 中，選取方案。  
  
2.  在 [檔案] 功能表上，指向 [新增]，再按一下 [新增專案]。  
  
3.  在 [新增專案] 對話方塊中，按一下某個專案類型。  
  
    **範本**  
    在 [範本] 方塊中，請選取一個範本。 選取的專案範本的簡短描述會出現在 [範本] 方塊以下。  
  
    **名稱**  
    請輸入您想要建立的指令碼專案名稱。 和專案具有相同名稱的資料夾也會建立於顯示在 [位置] 欄位中的位置。 針對某些專案，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 會建立來源以及其他支援檔案，並將它們加入新專案資料夾。  
  
    > [!NOTE]  
    > 針對某些專案類型，[名稱] 文字方塊無法使用，因為指定位置會設定名稱。 例如，Web 應用程式和 Web 服務位於 Web 伺服器上，並且從該伺服器上指定的虛擬目錄衍生出它們的名稱。  
  
    名稱不可包含以下字元：  
  
    -   井字號 (#)  
  
    -   百分比 (%)  
  
    -   連字號 (&)  
  
    -   星號 (*)  
  
    -   分隔號 (|)  
  
    -   反斜線 (\\)  
  
    -   冒號 (:)  
  
    -   引號 (")  
  
    -   小於 (\<)  
  
    -   大於 (>)  
  
    -   問號 (?)  
  
    -   斜線 (/)  
  
    -   開頭或尾端空白 (' ')  
  
    -   保留給 Microsoft Windows 或 MS-DOS 的名稱，例如 ("nul"、"aux"、"con"、"com1"、"lpt1" 等等)  
  
    **位置**  
    請輸入您想要建立專案的位置，或從清單中選擇。  
  
    **瀏覽**  
    顯示 [專案位置] 對話方塊，可以讓您導覽至新目錄以儲存專案。  
  
    **方案**  
    選取 [建立新方案]，即可在方案總管中建立方案。 選取 [新增至方案] 即可將新專案新增至方案總管中目前開啟的方案。  
  
    **建立方案的目錄**  
    選取以啟用 [(方案) 名稱] 文字方塊。 此選項會根據您為專案和方案選擇的名稱，來建立新的目錄。  
  
    **方案名稱**  
    輸入您希望在其中建立專案的新方案名稱。 依預設，此欄位會使用 [名稱] 欄位中輸入的名稱。  
  
    **請注意**：若要存取此選項，您必須同時選取 [方案] 中的 [建立新方案] 以及 [建立方案的目錄] 核取方塊。 有些專案範本 (例如 Web 應用程式) 不支援此選項。  
  
    **加入至原始檔控制**  
    如果選取此核取方塊，當您按一下 [確定] 時，原始檔控制應用程式就會開啟。 填妥原始檔控制應用程式所需的資訊之後，才能繼續。 您必須有安裝原始檔控制用戶端應用程式，才能使用此選項。  
  
4.  按一下 **[確定]**。  
  
您可以設定指令碼專案的名稱，但資料夾名稱由 [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 建立，無法變更。 您可以使用 [新增專案] 對話方塊，為一組常用資料夾設定磁碟和路徑規格。 在方案總管中，以滑鼠右鍵按一下方案，然後按一下 [新增]。 指令碼專案資料夾的預設位置是 C:\Documents and Settings\\<使用者名>\My Documents\SQL Server Management Studio\Projects\\。  
  
## <a name="see-also"></a>另請參閱  
[方案總管](../../ssms/solution/solution-explorer.md)  
[將現有專案加入方案中](../../ssms/solution/add-an-existing-project-to-a-solution.md)  
[將新項目加入專案](../../ssms/solution/add-new-items-to-a-project.md)  
[將現有的項目加入至專案](../../ssms/solution/add-existing-items-to-a-project.md)  
[變更專案的預設位置](../../ssms/solution/change-the-default-location-for-projects.md)  
[移除或刪除項目或專案](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
[刪除方案](../../ssms/solution/delete-a-solution.md)  
  

