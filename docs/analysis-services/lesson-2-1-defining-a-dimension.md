---
title: 定義維度 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 38185df9928286acf184fbad21fd75839856d017
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467922"
---
# <a name="lesson-2-1---defining-a-dimension"></a>課程 2-1-定義維度
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在下列工作中，您將使用「維度精靈」來建立「日期」維度。  
  
> [!NOTE]  
> 您必須先完成第 1 課的所有程序，才能進行這一課。  
  
### <a name="to-define-a-dimension"></a>定義維度  
  
1.  在方案總管中 (於 Microsoft Visual Studio 視窗右側)，以滑鼠右鍵按一下 [維度]，然後按一下 [新增維度]。 [維度精靈] 隨即出現。  
  
2.  在 [歡迎使用維度精靈] 頁面上，按一下 [下一步]。  
  
3.  在 [選取建立方法] 頁面上，確認已選取 [使用現有的資料表] 選項，然後按一下 [下一步]。  
  
4.  在 [指定來源資訊] 頁面上，確認已選取 **Adventure Works DW 2012** 資料來源檢視。  
  
5.  在 [主資料表] 清單中，選取 [日期]。  
  
6.  按一下 [下一步] 。  
  
7.  在 [選取維度屬性] 頁面上，選取下列屬性旁的核取方塊：  
  
    -   **日期索引鍵**  
  
    -   **完整日期替代索引鍵**  
  
    -   **英文月份**  
  
    -   **Calendar Quarter**  
  
    -   **Calendar Year**  
  
    -   **Calendar Semester**  
  
8.  將 [完整日期替代索引鍵] 屬性之 [屬性類型] 資料行的設定，從 [一般] 變更為 [日期]。 若要這樣做，請在 [屬性類型] 資料行中按一下 [一般]。 然後，按一下箭號，以便展開選項。 接著，按一下 [日期] > [日曆] > [日期]。 按一下 [確定] 。 重複這些步驟，即可變更屬性的屬性類型，如下所示：  
  
    -   [英文月份名稱] 變更為 [月]  
  
    -   [日曆季] 變更為 [季]  
  
    -   [日曆年度] 變更為 [年度]  
  
    -   [日曆半年度] 變更為 [半年]  
  
9. 按一下 [下一步] 。  
  
10. 在 [正在完成精靈] 頁面上，您可以在 [預覽] 窗格中看見 [日期] 維度及其屬性。  
  
11. 按一下 [完成] 以完成精靈。  
  
    在方案總管的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案中，[日期] 維度會顯示在 [維度] 資料夾中。 在開發環境的中心，維度設計師會顯示「日期」維度。  
  
12. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[定義 Cube](../analysis-services/lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>另請參閱  
[多維度模型中的維度](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
[使用現有的資料表建立維度](../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
[使用維度精靈建立維度](../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
  
