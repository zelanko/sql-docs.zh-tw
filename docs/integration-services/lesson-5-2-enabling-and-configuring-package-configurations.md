---
title: 步驟 2:啟用和設定套件設定 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 66388abaf9e1434abd78d595da25fc08ebeea1b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911516"
---
# <a name="lesson-5-2-enable-and-configure-package-configurations"></a>第 5-2 課：啟用和設定套件設定

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在此工作中，您會將專案轉換為套件部署模型，並使用 [套件設定精靈] 來啟用套件設定。 您會使用此精靈來產生 XML 設定檔，其中包含 Foreach 迴圈容器的 **Directory** 屬性組態設定。 **Directory** 屬性的值是由新套件層級變數提供，您可以在執行階段更新它。 您也會擴展一個要用於測試的新範例資料夾。  
  
## <a name="create-a-package-level-variable-mapped-to-the-directory-property"></a>建立一個對應至 Directory 屬性的套件層級變數  
  
1.  選取 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中 [控制流程]  索引標籤的背景。 此選項會將您建立的變數範圍設定為套件。  
  
2.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)]] 功能表上，選取 [變數]  。  
  
3.  在 [變數]  視窗中，選取**新增變數**圖示。  
  
4.  在 [名稱]  方塊中，輸入 **varFolderName**。  
  
    > [!IMPORTANT]  
    > 變數名稱會區分大小寫。  
  
5.  確認 [範圍]  方塊顯示套件的名稱，即**第 5 課**。  
  
6.  將 `varFolderName` 變數之 [資料類型]  方塊的值設定為 [字串]  。  
  
7.  回到 [控制流程]  索引標籤，按兩下 [資料夾的 Foreach 檔案]  容器。  
  
8.  在 [Foreach 迴圈編輯器]  的 [集合]  頁面上，選取 [運算式]  ，然後選取省略符號按鈕 **(...)** 。  
  
9. 在 [屬性運算式編輯器]  中，選取 [屬性]  清單，然後選取 [Directory]  。  
  
10. 在 [運算式]  方塊中，選取省略符號按鈕 **(...)** 。  
  
11. 在 [運算式產生器]  中，展開 [變數及參數]  資料夾，將 **User::varFolderName** 變數拖曳至 [運算式]  方塊。  
  
12. 選取 [確定]  以結束 [運算式產生器]  。  
  
13. 選取 [確定]  以結束 [屬性運算式編輯器]  。  
  
14. 選取 [確定]  以結束 [Foreach 迴圈編輯器]  。  
  
## <a name="enable-package-configurations"></a>啟用封裝組態  
  
1.  在 [專案]  功能表上，選取 [轉換為套件部署模型]  。  
  
2.  選取警告提示上的 [確定]  ，並在轉換完成時選取 [轉換為套件部署模型]  對話方塊中的 [確定]  。  
  
3.  選取 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中 [控制流程]  索引標籤的背景。  
  
4.  在 [SSIS]  功能表上，選取 [套件設定]  。  
  
5.  在 [套件設定組合管理]  對話方塊中，選取 [啟用套件設定]  ，然後選取 [新增]  。  
  
6.  在 [套件設定精靈]  的歡迎頁面上，選取 [下一步]  。  
  
7.  在 [選取組態類型]  頁面上，確認 [組態類型]  是設為 [XML 組態檔]  。  
  
8.  在 [選取設定類型]  頁面上，選取 [瀏覽]  。  
  
9. [選取設定檔位置]  對話方塊會開啟至專案資料夾。  
  
10. 在 [選取設定檔位置]  對話方塊的 [檔案名稱]  中，輸入 **SSISTutorial**，然後選取 [儲存]  。  
  
11. 在 [選取設定類型]  頁面上，選取 [下一步]  。
  
12. 在 [選取要匯出的屬性]  頁面的 [物件]  窗格中，依序展開 [變數]  、[varFolderName]  和 [屬性]  ，然後選取 [值]  。  
  
13. 在 [選取要匯出的屬性]  頁面上，選取 [下一步]  。  
  
14. 在 [正在完成精靈]  頁面上，輸入設定的設定名稱，例如 **SSIS 教學課程目錄設定**。 此設定名稱會顯示在 [套件設定組合管理]  對話方塊中。  
  
15. 選取 [完成]  。  
  
16. 選取 [關閉]  。  
  
17. 精靈會建立一個名為 **SSISTutorial.dtsConfig** 的設定檔，其中包含變數的 **Value** 組態設定，再由這個變數設定列舉值的 **Directory** 屬性。  
  
    > [!NOTE]  
    > 設定檔通常包含關於套件屬性的複雜資訊，但在此教學課程中，唯一的設定資訊應該如下所示：

    ```
    <Configuration 
        ConfiguredType="Property"  
        Path="\Package.Variables[User::varFolderName].Properties[Value]" 
        ValueType="String">  
      <ConfiguredValue></ConfiguredValue>  
    </Configuration>
    ```
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>建立並填入新的範例資料夾  
  
1.  在 Windows 檔案總管中，於磁碟機的根目錄層級 (例如 **C:\\** ) 建立一個名為 **New Sample Data** 的資料夾。  
  
2.  尋找電腦上的範例檔案，並從資料夾複製三個檔案。  
  
3.  在 **New Sample Data** 資料夾，貼上已複製的檔案。  
  
## <a name="go-to-next-task"></a>移至下一個工作  
[步驟 3：修改 Directory 屬性設定值](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
