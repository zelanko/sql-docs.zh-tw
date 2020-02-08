---
title: 步驟 4：將資料流程工作新增至套件 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a98437a88fc81d83c98ec2c3417df6d38bc1b421
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283828"
---
# <a name="lesson-1-4-add-a-data-flow-task-to-the-package"></a>第 1-4 課：將資料流程工作新增至套件

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在建立來源和目的地資料的連線管理員之後，要將資料流程工作新增到套件。 資料流程工作會定義在來源和目的地之間移動資料的資料流程引擎，以及提供轉換、清理和修改移動中資料的功能。 資料流程工作是進行擷取、轉換和載入 (ETL) 處理序大部份工作之處。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會將資料流程與控制流程分開。  
  
## <a name="add-a-data-flow-task"></a>新增資料流程工作  
  
1.  選取 [控制流程]  索引標籤。  
  
2.  在 [SSIS 工具箱]  中，展開 [我的最愛]  ，然後將 [資料流程工作]  拖曳至 [控制流程]  索引標籤的設計介面中。  
  
    > [!NOTE]  
    > 如果 SSIS 工具箱無法使用，請選取 [SSIS]  功能表，然後選取 [SSIS 工具箱]  予以顯示。  

3.  在 [控制流程]  設計介面上，以滑鼠右鍵按一下新的 [資料流程工作]  ，選取 [重新命名]  ，將名稱變更為 **Extract Sample Currency Data**。  
  
    為您新增到設計界面的所有元件都提供唯一名稱。 為了使用和維護上的方便，名稱應該要描述各個元件的功能。 遵照這些命名指導方針可讓 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 套件自我記錄。 記錄封裝的另一個方法是使用註解。 如需註解的詳細資訊，請參閱 [在套件中使用註解](../integration-services/use-annotations-in-packages.md)。  
  
4.  以滑鼠右鍵按一下資料流程工作，選取 [屬性]  ，然後在 [屬性] 視窗中，確認 **LocaleID** 屬性設為 [英文 (美國)]  。  
  
## <a name="go-to-next-task"></a>移至下一個工作
[步驟 5：新增及設定一般檔案來源](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>另請參閱  
[資料流程工作](../integration-services/control-flow/data-flow-task.md)  
  
  
  
