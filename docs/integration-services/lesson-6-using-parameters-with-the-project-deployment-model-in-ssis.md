---
title: 第 6 課：在 SSIS 中搭配專案部署模型使用參數 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 54fb96d23fb02be01068ce5c2206913a0e6716f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721056"
---
# <a name="lesson-6-use-parameters-with-the-project-deployment-model-in-ssis"></a>第 6 課：在 SSIS 中搭配專案部署模型使用參數

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server 2012 引進了新的部署模型，讓您可以將專案部署到 Integration Services 伺服器。 Integration Services 伺服器可讓您管理及執行封裝，以及設定封裝的執行值。  
  
在本課程中，您會修改在[第 5 課：新增套件部署模型的 SSIS 套件設定](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)中所建立套件，以便使用專案部署模型。 您會以參數取代組態值來指定範例資料位置。 您也可以複製此教學課程所包含之已完成的第 5 課封裝。  
  
藉由使用 [Integration Services 專案設定精靈]，您可以將專案轉換為專案部署模型。 此模型使用參數 (而非設定值) 來設定 Directory 屬性。 這一課的部分內容涵蓋了將現有的 SSIS 封裝轉換成新專案部署模型的步驟。  
  
當您重新執行套件時，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器會使用參數來填入變數的值。 該變數接著會更新 Directory 屬性。 套件會反覆執行新參數所指定資料夾中的檔案。  
  
> [!NOTE]
> 如果您尚未這麼做，請參閱[第 1 課的先決條件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)。
    
## <a name="lesson-tasks"></a>課程工作  
這一課包含下列工作：  
  
1.  [步驟 1：複製第 5 課套件](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [步驟 2：將專案轉換為專案部署模型](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [步驟 3：測試第 6 課套件](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [步驟 4：部署第 6 課套件](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>開始課程  
[步驟 1：複製第 5 課套件](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
