---
title: 步驟 1：複製第 1 課套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e0373918efff503779e139bb21efad58549b3850
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440645"
---
# <a name="step-1-copying-the-lesson-1-package"></a>步驟 1:複製第 1 課的封裝
  在這項工作中，您將為第 1 課所建立的 Lesson 1.dtsx 套件建立複本。 如果您並未完成第 1 課，可以將此教學課程中隨附之已完成的第 1 課封裝加入至專案中，然後改為複製該封裝。 在第 2 課其餘的課程中，您將使用這個新的複本。  
  
### <a name="to-create-the-lesson-2-package"></a>若要建立第 2 課的封裝  
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未開啟，請按一下 [開始]****，並依序指向 [所有程式]**** 和 [Microsoft SQL Server 2012]****，然後按一下 [SQL Server Data Tools]****。  
  
2.  在 [檔案]**** 功能表上，依序按一下 [開啟]****、[專案/方案]**** 和 [SSIS 教學課程]**** 資料夾，然後按一下 [開啟]****，再按兩下 [SSIS Tutorial.sln]****。  
  
3.  在方案總管中，以滑鼠右鍵按一下 [Lesson 1.dtsx]****，然後按一下 [複製]****。  
  
4.  在方案總管中，以滑鼠右鍵按一下 [ **SSIS 封裝**]，然後按一下 [**貼**上]。  
  
     依預設，所複製的封裝稱為 Lesson 2.dtsx。  
  
5.  在方案總管中，按兩下**第2課**以開啟封裝  
  
6.  以滑鼠右鍵按一下 [控制流程]**** 設計介面背景的任何位置，然後按一下 [屬性]****。  
  
7.  在屬性視窗中，將 `Name` 屬性更新為 `Lesson 2` 。  
  
8.  按一下 [ID]**** 屬性的方塊，並按一下下拉箭頭，然後按一下 **\<Generate New ID>**。  
  
### <a name="to-add-the-completed-lesson-1-package"></a>新增已完成的第 1 課套件  
  
1.  開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 及 SSIS 教學課程專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [ **SSIS 封裝**]，然後按一下 [**新增現有套件**]。  
  
3.  在 [**加入現有封裝的副本**] 對話方塊的 [**封裝位置**] 中，選取 [**檔案系統**]。  
  
4.  按一下瀏覽 **(…)** 按鈕，巡覽至電腦上的 **Lesson 1.dtsx**，然後按一下 [開啟]****。  
  
     若要下載此教學課程的所有課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  按一下 [**下載**] 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
5.  複製並貼上第 1 課套件，如上一個程序的步驟 3-8 所述。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 2:新增和設定 Foreach 迴圈容器](lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
  
