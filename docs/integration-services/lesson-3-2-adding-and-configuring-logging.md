---
title: 步驟 2:新增及設定記錄 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e2b43837de8617af559e2a810c89115e5a3963d3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283264"
---
# <a name="lesson-3-2-add-and-configure-logging"></a>課程 3-2：新增及設定記錄

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在此工作中，您會針對 Lesson 3.dtsx 套件中的資料流程啟用記錄。 然後，您會設定「文字檔」記錄提供者來記錄 PipelineExecutionPlan 和 PipelineExecuteTrees 事件。 「文字檔」記錄提供者會建立容易檢視及傳輸的記錄。 由於這些記錄檔的簡單性，使得它們在套件的基本測試階段相當有用。 您也可以在「[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計工具」的 [記錄事件]  視窗中檢視記錄項目。  
  
## <a name="add-logging-to-the-package"></a>將記錄新增至套件中  
  
1.  在 [SSIS]  功能表上，選取 [記錄]  。  
  
2.  在 **[設定 SSIS 記錄]** 對話方塊的 [容器]  窗格中，確定已選取最上層物件。 此物件代表第 3 課套件。
  
3.  在 [提供者與記錄]  索引標籤的 [提供者類型]  方塊中，選取 [文字檔的 SSIS 記錄提供者]  ，然後按一下 [加入]  。  
  
    Integration Services 會以預設名稱**文字檔的 SSIS 記錄提供者**，將新的「文字檔」記錄提供者新增至套件中。 現在您可以設定新的記錄提供者。  
  
4.  在 [名稱]  資料行中，輸入**第 3 課記錄檔**。  
  
5.  可選擇性地修改 **[描述]** 。  
  
6.  在 [設定]  資料行中，選取 [\<新連接>]  以指定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 寫入記錄資訊的位置。  
  
    在 [檔案連線管理員編輯器]  對話方塊中，針對 [使用類型]  選取 [建立檔案]  ，然後選取 [瀏覽]  。 [選取檔案]  對話方塊預設會開啟專案資料夾，但您可以將記錄資訊儲存至任何位置。  
  
7.  在 [選取檔案]  對話方塊的 [檔案名稱]  方塊中，輸入 **TutorialLog.log**，然後選取 [開啟]  。
  
8.  選取 [確定]  以關閉 [檔案連線管理員編輯器]  對話方塊。  
  
9. 在 **[容器]** 窗格中，展開封裝容器階層的所有節點，然後清除所有核取方塊，包括 **[擷取範例貨幣資料]** 核取方塊在內。 現在，請選取 **[擷取範例貨幣資料]** 來取得只有此節點的事件。  
  
    > [!NOTE]  
    > 如果 [擷取範例貨幣資料]  核取方塊的狀態呈現暗灰色而不是已選取，即表示此工作使用父容器的記錄設定，您無法啟用此工作特定的記錄事件。 若要解決這種情況，請將父核取方塊取消選取。
  
10. 在 **[詳細資料]** 索引標籤的 **[事件]** 資料行中，選取 **[PipelineExecutionPlan]** 和 **[PipelineExecutionTrees]** 事件。  
  
11. 選取 [進階]  以檢閱記錄提供者針對每個事件寫入記錄檔的詳細資料。 依預設，對於您指定的事件，會自動選取所有資訊類別目錄。  
  
12. 選取 [基本]  以隱藏資訊類別目錄。  
  
13. 在 **[提供者與記錄]** 索引標籤的 **[名稱]** 資料行中，選取 **[第 3 課記錄檔]** 。 為套件建立記錄提供者之後，您可以視需要將其取消選取來關閉記錄，而不必刪除再重新建立記錄提供者。  
  
14. 選取 [確定]  。  
  
## <a name="go-to-next-task"></a>移至下一個工作  
[步驟 3：測試第 3 課套件](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
