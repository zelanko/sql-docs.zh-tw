---
title: 步驟 1：複製第 2 課的封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 4bd91402-4e37-41de-ab78-8ca5a1948a37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2cc63345e757ca07490a6bf365c2523ccda8b0c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761446"
---
# <a name="lesson-3-1---copying-the-lesson-2-package"></a>課程 3-1 - 複製第 2 課的封裝
在這項工作中，您將為第 2 課所建立的 Lesson 2.dtsx 套件建立複本。 另外，您也可以將此教學課程中隨附之已完成的第 2 課套件加入專案，然後改為複製該套件。 在第 3 課其餘的課程中，您將使用這個新的複本。  
  
### <a name="to-create-the-lesson-3-package"></a>建立第 3 課的套件  
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未開啟，請按一下 [開始]，依序指向 [所有程式] 和 [Microsoft SQL Server 2012]，然後按一下 [SQL Server Data Tools]。  
  
2.  在 [檔案] 功能表上，依序按一下 [開啟] 和 [專案/方案]，選取 [SSIS 教學課程]，然後按一下 [開啟]，再按兩下 **SSIS Tutorial.sln**。  
  
3.  在方案總管中，以滑鼠右鍵按一下 **Lesson 2.dtsx**，然後按一下 [複製]。  
  
4.  在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]，然後按一下 [貼上]。  
  
    依預設，所複製的套件稱為 Lesson 3.dtsx。  
  
5.  在方案總管中，按兩下 **Lesson 3.dtsx** 來開啟套件。  
  
6.  以滑鼠右鍵按一下 [控制流程] 索引標籤背景的任何位置，然後按一下 [屬性]。  
  
7.  在 [屬性] 視窗中，將 [名稱] 屬性更新為**第 3 課**。  
  
8.  按一下 [識別碼] 屬性的方塊，然後在清單中按一下 [<Generate New ID>]。  
  
### <a name="to-add-the-completed-lesson2-package"></a>若要加入已完成的第 2 課封裝  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 及開啟 SSIS 教學課程專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]，然後按一下 [加入現有的封裝]。  
  
3.  在 [加入現有封裝的複本] 對話方塊的 [封裝位置] 中，選取 [檔案系統]。  
  
4.  按一下瀏覽 **(…)** 按鈕，巡覽至電腦上的 **Lesson 2.dtsx**，然後按一下 [開啟]。  
  
    若要下載此教學課程的所有課程封裝，請執行下列動作。  
  
    1.  導覽至 [Integration Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  按一下 **[下載]** 索引標籤。  
  
    3.  按一下 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 檔案。  
  
5.  複製並貼上第 3 課中的套件，如上一個程序的步驟 3-8 所述。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[步驟 2：新增和設定記錄](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
