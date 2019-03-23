---
title: 步驟 4：將資料流程工作新增至套件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 542b7e3ffcc4a1db5b2053c840b785f775384fe1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381186"
---
# <a name="step-4-adding-a-data-flow-task-to-the-package"></a>步驟 4：將資料流程工作加入至封裝中
  在建立來源和目的地資料的連接管理員之後，下一項工作是將資料流程工作加入封裝中。 資料流程工作封裝資料流程引擎，它在來源和目的地之間移動資料，以及提供轉換、清理和修改移動中資料的功能。 資料流程工作是進行擷取、轉換和載入 (ETL) 處理序大部份工作之處。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 將資料流程與控制流程。  
  
### <a name="to-add-a-data-flow-task"></a>若要加入資料流程工作  
  
1.  按一下 **[控制流程]** 索引標籤。  
  
2.  在 [SSIS 工具箱] 中，展開 [我的最愛]，然後將 [資料流程工作] 拖曳至 [控制流程] 索引標籤的設計介面中。  
  
    > [!NOTE]  
    >  如果 [SSIS 工具箱] 無法使用，請在主功能表上，依序選取 [SSIS] 和 [SSIS 工具箱]，即可顯示 [SSIS 工具箱]。  
  
3.  在上**控制流程**設計介面上，以滑鼠右鍵按一下 新增**Data Flow Task**，按一下 **重新命名**，並將名稱變更為`Extract Sample Currency Data`。  
  
     提供唯一名稱給所有您要加入設計介面中的元件，是不錯的作法。 為了使用和維護上的方便，名稱應該要描述每一個元件執行的功能。 遵照這些命名指導方針可讓 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件自我記錄。 記錄封裝的另一個方法是使用註解。 如需使用註解的詳細資訊，請參閱 [在套件中使用註解](use-annotations-in-packages.md)。  
  
4.  以滑鼠右鍵按一下 資料流程工作中，按一下**屬性**，然後在 屬性 視窗中，確認`LocaleID`屬性設定為**英文 （美國）**。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [步驟 5：新增和設定一般檔案來源](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程工作](control-flow/data-flow-task.md)  
  
  
