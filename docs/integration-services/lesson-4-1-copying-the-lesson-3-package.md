---
title: 步驟 1：複製第 3 課的封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0d053786-5203-43f3-a613-27a8dd2bc44a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ce3f4e559e9ed708154b8c5b5710540c701b44e
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51638495"
---
# <a name="lesson-4-1---copying-the-lesson-3-package"></a>課程 4-1 - 複製第 3 課的封裝
在這項工作中，您將為第 3 課所建立的 Lesson 3.dtsx 套件建立複本。 另外，如果您並未完成第 3 課，可以將此教學課程中隨附之已完成的第 3 課封裝加入至專案中，然後建立該封裝的複本來使用。 在第 4 課的其餘課程中，您將使用這個新的複本。  
  
### <a name="to-create-the-lesson-4-package"></a>建立第 4 課的套件  
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未開啟，請按一下 [開始]，並依序指向 [所有程式] 和 [Microsoft SQL Server]，然後按一下 [SQL Server Data Tools]。  
  
2.  在 [檔案] 功能表上，依序按一下 [開啟] 和 [專案/方案]，選取 [SSIS 教學課程]，再按一下 [開啟]，然後按兩下 **SSIS Tutorial.sln**。  
  
3.  在方案總管中，以滑鼠右鍵按一下 **Lesson 3.dtsx**，然後按一下 [複製]。  
  
4.  在方案總管中，以滑鼠右鍵按一下 [SSIS 套件]，然後按一下 [貼上]。  
  
    依預設，所複製的套件稱為 Lesson 4.dtsx。  
  
5.  在方案總管中，按兩下 [Lesson 4.dtsx] 來開啟套件。  
  
6.  以滑鼠右鍵按一下 [控制流程] 索引標籤背景的任何位置，然後按一下 [屬性]。  
  
7.  在 [屬性] 視窗中，將 [名稱] 屬性更新為 [第 4 課]。  
  
8.  按一下 [識別碼] 屬性的方塊，然後在清單中按一下 [<Generate New ID>]。  
  
### <a name="to-add-the-completed-lesson-3-package"></a>新增已完成的第 3 課套件  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 及開啟 SSIS 教學課程專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]，然後按一下 [加入現有的封裝]。  
  
3.  在 [加入現有封裝的複本] 對話方塊的 [封裝位置] 中，選取 [檔案系統]。  
  
4.  按一下瀏覽 **(…)** 按鈕，巡覽至電腦上的 Lesson 3.dtsx，然後按一下 [開啟]。  
  
    若要下載此教學課程的所有課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
5.  複製並貼上第 3 課中的套件，如上一個程序的步驟 3-8 所述。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 2：建立損毀檔案](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
