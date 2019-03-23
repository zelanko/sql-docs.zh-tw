---
title: 步驟 1：複製第 2 課套件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b4458f8fe198ba3d052bcb21bef38975738b2c23
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381226"
---
# <a name="step-1-copying-the-lesson-2-package"></a>步驟 1：複製第 2 課的套件
  在這項工作中，您將為第 2 課所建立的 Lesson 2.dtsx 套件建立複本。 另外，您也可以將此教學課程中隨附之已完成的第 2 課套件加入專案，然後改為複製該套件。 在第 3 課其餘的課程中，您將使用這個新的複本。  
  
### <a name="to-create-the-lesson-3-package"></a>建立第 3 課的套件  
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未開啟，請按一下 [開始]，依序指向 [所有程式] 和 [Microsoft SQL Server 2012]，然後按一下 [SQL Server Data Tools]。  
  
2.  在 [檔案] 功能表上，依序按一下 [開啟] 和 [專案/方案]，選取 [SSIS 教學課程]，然後按一下 [開啟]，再按兩下 **SSIS Tutorial.sln**。  
  
3.  在方案總管中，以滑鼠右鍵按一下 **Lesson 2.dtsx**，然後按一下 [複製]。  
  
4.  在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]，然後按一下 [貼上]。  
  
     依預設，所複製的套件稱為 Lesson 3.dtsx。  
  
5.  在方案總管中，按兩下 **Lesson 3.dtsx** 來開啟套件。  
  
6.  以滑鼠右鍵按一下 [控制流程] 索引標籤背景的任何位置，然後按一下 [屬性]。  
  
7.  在 [屬性] 視窗中，更新`Name`屬性設`Lesson 3`。  
  
8.  按一下方塊**識別碼**屬性，然後在清單中，按一下**\<產生新的識別碼 >**。  
  
### <a name="to-add-the-completed-lesson2-package"></a>若要加入已完成的第 2 課封裝  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 及開啟 SSIS 教學課程專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]，然後按一下 [加入現有的封裝]。  
  
3.  在 [加入現有封裝的複本] 對話方塊的 [封裝位置] 中，選取 [檔案系統]。  
  
4.  按一下瀏覽 **(…)** 按鈕，巡覽至電腦上的 **Lesson 2.dtsx**，然後按一下 [開啟]。  
  
     若要下載此教學課程的所有課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
5.  複製並貼上第 3 課中的套件，如上一個程序的步驟 3-8 所述。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 2：加入和設定記錄](lesson-3-2-adding-and-configuring-logging.md)  
  
  
