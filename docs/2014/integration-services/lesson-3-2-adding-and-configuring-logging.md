---
title: 步驟 2:加入和設定記錄 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ef4f5d42ae3451d4199e84480a5672e437d7ca5f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62892433"
---
# <a name="step-2-adding-and-configuring-logging"></a>步驟 2:加入和設定記錄
  在這項工作中，您將針對 Lesson 3.dtsx 封裝的資料流程啟用記錄。 然後，您會設定文字檔案記錄提供者來記錄 PipelineExecutionPlan 和 PipelineExecuteTrees 事件。 文字檔案記錄提供者會建立容易檢視及容易傳輸的記錄。 這些記錄檔的簡單性，使它們在封裝的基本測試階段特別有用。 您也可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師的 [記錄事件] 視窗中檢視記錄項目。  
  
### <a name="to-add-logging-to-the-package"></a>若要將記錄加入封裝中  
  
1.  在 **[SSIS]** 功能表上，按一下 **[記錄]**。  
  
2.  在 **[設定 SSIS 記錄]** 對話方塊的 **[容器]** 窗格中，確定有選取代表第 3 課封裝的最上層物件。  
  
3.  在 **[提供者與記錄]** 索引標籤的 **[提供者類型]** 方塊中，選取 **[文字檔的 SSIS 記錄提供者]**，然後按一下 **[加入]**。  
  
     Integration Services 以預設名稱 **「文字檔的 SSIS 記錄提供者」**，將新的文字檔記錄提供者加入封裝中。 現在您可以設定新的記錄提供者。  
  
4.  在 **名稱**資料行中輸入`Lesson 3 Log File`。  
  
5.  可選擇性地修改 **[描述]**。  
  
6.  在**組態**資料行中，按一下**\<新增連接 >** 指定記錄資訊會寫入至其中的目的地。  
  
     在 **[檔案連接管理員編輯器]** 對話方塊中，對於 **[使用類型]** 選取 **[建立檔案]**，然後按一下 **[瀏覽]**。 依預設， **[選取檔案]** 對話方塊會開啟專案資料夾，但您可以將記錄資訊儲存至任何位置。  
  
7.  在**選取檔案**對話方塊中，於**檔案名稱**方塊中，輸入`TutorialLog.log`，然後按一下**開啟**。  
  
8.  按一下 **[確定]** 來關閉 **[檔案連接管理員編輯器]** 對話方塊。  
  
9. 在 **[容器]** 窗格中，展開封裝容器階層的所有節點，然後清除所有核取方塊，包括 **[擷取範例貨幣資料]** 核取方塊在內。 現在，請選取 **[擷取範例貨幣資料]** 來取得只有此節點的事件。  
  
    > [!IMPORTANT]  
    >  如果 **[擷取範例貨幣資料]** 核取方塊呈現暗灰色而不是被選取，此工作將使用父容器的記錄設定，且您不能啟用此工作特定的記錄事件。  
  
10. 在 **[詳細資料]** 索引標籤的 **[事件]** 資料行中，選取 **[PipelineExecutionPlan]** 和 **[PipelineExecutionTrees]** 事件。  
  
11. 按一下 **[進階]** 來檢閱記錄提供者將針對每一個事件寫入記錄檔的詳細資料。 依預設，對於您指定的事件，會自動選取所有資訊類別目錄。  
  
12. 按一下 **[基本]** 來隱藏資訊類別目錄。  
  
13. 在 **提供者與記錄**索引標籤中，於**名稱**欄中，選取`Lesson 3 Log File`。 建立封裝的記錄提供者之後，您就可以選擇性地取消選取它，來暫時關閉記錄，而不必刪除再重新建立記錄提供者。  
  
14. 按一下 [確定] 。  
  
## <a name="next-steps"></a>後續步驟  
 [步驟 3：測試第 3 課的教學課程封裝](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
  
