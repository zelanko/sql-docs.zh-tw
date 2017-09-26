---
title: "步驟 1： 複製第 5 課封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: a25fcc13-987e-4f3d-8f0c-76f7e6e59920
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6de5c21ac26411f39ae6d46a1fd1824f73d5c3b7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-6-1---copying-the-lesson-5-package"></a>課程 6-1-複製第 5 課封裝
在這項工作中，您將為第 5 課所建立的 Lesson 5.dtsx 封裝建立複本。 另外，您也可以將此教學課程中隨附之已完成的第 5 課封裝加入至專案中，然後改為複製該封裝。 在第 6 課其餘的課程中，您將使用這個新的副本。  
  
### <a name="to-copy-the-lesson-5-package"></a>若要複製第 5 課的封裝  
  
1.  如果 SQL Server Data Tools 尚未開啟，請按一下 [開始]，依序指向 [所有程式] 和 [Microsoft SQL Server 2012]，然後按一下 [SQL Server Data Tools]。  
  
2.  在 [檔案] 功能表上，依序按一下 [開啟] 和 [專案/方案]，選取 [SSIS 教學課程]，然後按一下 [開啟]，再按兩下 SSIS Tutorial.sln。  
  
3.  在 [方案總管] 中，以滑鼠右鍵按一下 Lesson 5.dtsx，然後按一下 [複製]。  
  
4.  在 [方案總管] 中，以滑鼠右鍵按一下 [SSIS 封裝]，然後按一下 [貼上]。  
  
    依預設，所複製的封裝稱為 Lesson 6.dtsx。  
  
5.  在 [方案總管] 中，按兩下 Lesson 6.dtsx 來開啟封裝。  
  
6.  以滑鼠右鍵按一下 [控制流程] 索引標籤背景的任何位置，然後按一下 [屬性]。  
  
7.  在 [屬性] 視窗中，將 Name 屬性更新為第 6 課。  
  
8.  依序按一下 ID 屬性的方塊、下拉箭頭及 [ <Generate New ID>]。  
  
### <a name="to-add-the-completed-lesson-5-package"></a>若要加入已完成的第 5 課封裝  
  
1.  開啟 SQL Server Data Tools 及 SSIS 教學課程專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下 [SSIS 封裝]，然後按一下 [加入現有的封裝]。  
  
3.  在 [加入現有封裝的副本] 對話方塊的 [封裝位置] 中，選取 [檔案系統]。  
  
4.  按一下瀏覽 (…) 按鈕，巡覽至電腦上的 Lesson 5.dtsx，然後按一下 [開啟]。  
  
    若要下載此教學課程的所有課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
5.  複製並貼上第 5 課封裝，如上一個程序的步驟 3-8 所述。  
  
    在複製第 5 課封裝之後，如果您目前在方案中已經有之前課程的封裝，請以滑鼠右鍵按一下 1-5 課的每一個封裝，並按一下 [從專案移除]。 當您完成時，您的方案中應該只有 Lesson 6.dtsx。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 2：將專案轉換成專案部署模型](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  

