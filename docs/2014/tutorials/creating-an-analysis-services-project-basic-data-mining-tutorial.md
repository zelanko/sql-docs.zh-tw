---
title: 建立 Analysis Services 專案 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 784c0401-0358-4117-9c85-4e8220ce71d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ee6c1a8b765843304d25f1e2ad485ede2badcba4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855189"
---
# <a name="creating-an-analysis-services-project-basic-data-mining-tutorial"></a>建立 Analysis Services 專案 (基本資料採礦教學課程)
  每個 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案都會在單一 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中定義物件。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫可包含許多不同類型的物件  
  
-   多維度模型 (Cube)  
  
-   採礦結構和採礦模型  
  
-   提供支援的物件，例如資料來源、資料來源檢視和自訂組件  
  
 請注意，您 **不需要** Cube 便能進行資料採礦。 如果您必須對現有的 Cube 進行資料採礦，就應該將資料採礦模型加入至您用來建立 Cube 的相同專案。 不過，大多數的用途情況下您都能根據關聯式資料來源 (例如資料倉儲) 建立模型，只要不涉及 Cube 即可有更好的效能。  
  
 在本教學課程中，您將使用關聯式資料倉儲 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]做為資料來源。 您會將所有的資料採礦物件部署到名稱為 `BasicDataMining` 的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，僅供用於資料採礦。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 預設會針對新專案使用 **localhost** 執行個體。 如果您要使用具名執行個體或不同的伺服器，您必須先建立並開啟專案，然後變更執行個體名稱。  
  
 如需詳細資訊[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]專案，請參閱[建立 Analysis Services 專案](../analysis-services/lesson-1-1-creating-an-analysis-services-project.md)。  
  
### <a name="to-create-an-analysis-services-project"></a>若要建立 Analysis Services 專案  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
2.  在 **[檔案]** 功能表上，指向 **[開新檔案]**，再選取 **[專案]**。  
  
3.  確認 **[專案類型]** 窗格中已選取 **[商業智慧專案]** 。  
  
4.  在 **[範本]** 窗格中，選取 **[Analysis Services 多維度和資料採礦專案]**。  
  
5.  在 **名稱**方塊中，將新專案命名`BasicDataMining`。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored"></a>變更儲存資料採礦物件所在的執行個體  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的 **[專案]** 功能表上，選取 **[屬性]**。  
  
2.  在 **[屬性頁]** 窗格左邊的 **[組態屬性]** 底下，按一下 **[部署]**。  
  
3.  在 **[屬性頁]** 窗格右邊的 **[目標]** 底下，確認 **[伺服器]** 名稱是 **localhost**。 如果您要使用不同的執行個體，請輸入執行個體的名稱。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立資料來源&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [建立 Analysis Services 專案 &#40;SSDT&#41;](../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [建立 Analysis Services 專案 &#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
