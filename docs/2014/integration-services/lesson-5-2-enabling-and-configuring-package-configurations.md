---
title: 步驟 2：啟用和設定封裝組態 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa75b3a71832eaba4064de5a9dd90e73236e8177
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378206"
---
# <a name="step-2-enabling-and-configuring-package-configurations"></a>步驟 2：啟用和設定封裝組態
  在此工作中，您會將專案轉換成封裝部署模型，並使用封裝組態精靈來啟用封裝組態。 您將利用這個精靈來產生 XML 組態檔，它包含 Foreach 迴圈容器的 `Directory` 屬性的組態設定。 Directory 屬性的值是由新的封裝層級變數提供，您可以在執行階段更新它。 另外，您還會擴展一個要在測試期間使用的新範例資料夾。  
  
### <a name="to-create-a-new-package-level-variable-mapped-to-the-directory-property"></a>若要建立一個對應至 Directory 屬性的新封裝層級變數  
  
1.  按一下 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 的 [控制流程] 索引標籤的背景。 這樣會將您要建立之變數的範圍設定為封裝。  
  
2.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)]] 功能表上，選取 [變數]。  
  
3.  在 [變數] 視窗中，按一下加入變數圖示。  
  
4.  在 [名稱] 方塊中，輸入 **varFolderName**。  
  
    > [!IMPORTANT]  
    >  變數名稱會區分大小寫。  
  
5.  確認 [範圍] 方塊顯示套件的名稱，即「第 5 課」。  
  
6.  將 `varFolderName` 變數之 [資料類型] 方塊的值設定為 [字串]。  
  
7.  回到 [控制流程] 索引標籤，按兩下 [資料夾的 Foreach 檔案] 容器。  
  
8.  在 [Foreach 迴圈編輯器] 的 [集合] 頁面上，按一下 [運算式]，然後按一下省略符號按鈕 **(...)**。  
  
9. 在 **屬性運算式編輯器**，按一下**屬性**清單，並選取`Directory`。  
  
10. 在 **運算式**方塊中，按一下省略符號按鈕 **（...）**.  
  
11. 在 [運算式產生器] 中，展開 [變數] 資料夾，將 **User::varFolderName** 變數拖曳至 [運算式] 方塊中。  
  
12. 按一下 [確定] 來結束 [運算式產生器]。  
  
13. 按一下 [確定] 來結束 [屬性運算式編輯器]。  
  
14. 按一下 [確定] 來結束 [Foreach 迴圈編輯器]。  
  
### <a name="to-enable-package-configurations"></a>若要啟用封裝組態  
  
1.  在 [專案] 功能表上，按一下 [轉換為封裝部署模型]。  
  
2.  按一下警告提示上的 [確定]，並在轉換完成時按一下 [轉換為封裝部署模型] 對話方塊上的 [確定]。  
  
3.  按一下 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 的 [控制流程] 索引標籤的背景。  
  
4.  在 [SSIS] 功能表上，按一下 [封裝組態]。  
  
5.  在 [封裝組態組合管理] 對話方塊中，選取 [啟用封裝組態]，然後按一下 [加入]。  
  
6.  在 [封裝組態精靈] 的歡迎使用頁面上，按一下 [下一步]。  
  
7.  在 [選取組態類型] 頁面上，確認 [組態類型] 是設為 [XML 組態檔]。  
  
8.  在 [選取組態類型] 頁面上，按一下 [瀏覽]。  
  
9. 根據預設，[選取組態檔位置] 對話方塊開啟時將顯示專案資料夾。  
  
10. 在 [選取組態檔位置] 對話方塊的 [檔案名稱] 中，輸入 **SSISTutorial**，然後按一下 [儲存]。  
  
11. 在 [選取組態類型] 頁面上，按一下 [下一步]。  
  
12. 在 [選取要匯出的屬性] 頁面的 [物件] 窗格中，依序展開 [變數]、[varFolderName] 和 [屬性]，然後選取 [值]。  
  
13. 在 [選取要匯出的屬性] 頁面上，按一下 [下一步]。  
  
14. 在 [正在完成精靈] 頁面上，輸入組態的組態名稱，例如 **SSIS 教學課程目錄組態**。 這是顯示在 [封裝組態組合管理] 對話方塊中的組態名稱。  
  
15. 按一下 **[完成]**。  
  
16. 按一下 [ **關閉**]。  
  
17. 精靈會建立組態檔，稱為 SSISTutorial.dtsConfig，其中包含組態設定，如`value`所設定的變數`Directory`列舉值的屬性。  
  
    > [!NOTE]  
    >  組態檔通常包含關於封裝屬性的複雜資訊，但在此教學課程中，唯一的組態資訊應該是  
    > <Configuration ConfiguredType="Property"  
    > Path="\Package.Variables[User::varFolderName]。ValueType 屬性 [Value] ="String"\>  
    >  \<ConfiguredValue>\</ConfiguredValue>  
    > \</ 組態 >。  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>若要建立及擴展新的範例資料夾  
  
1.  在 Windows 檔案總管，於您的磁碟機的根層級 (例如 c:\\)，建立新的資料夾，名為`New Sample Data`。  
  
2.  尋找電腦上的範例檔案，並從資料夾複製三個檔案。  
  
3.  在 `New Sample Data`資料夾中，貼上複製的檔案。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 3：修改 Directory 屬性組態值](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
  
