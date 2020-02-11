---
title: 啟用 DirectQuery 設計模式（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 965a3a7c1bfa9549793690e92760ce39f147e0d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067200"
---
# <a name="enable-directquery-design-mode-ssas-tabular"></a>啟用 DirectQuery 設計模式 (SSAS 表格式)
  若要建立 DirectQuery 模式的模型，必須先將設計階段環境變更為支援使用 DirectQuery 模式。 當您這樣做時，設計工具還會執行下列操作：  
  
-   啟用 DirectQuery 部署屬性。  
  
-   將工作空間資料庫變更為以混合模式執行，以使用快取進行設計。 在您實際部署模型時，模式會變更回您在專案部署屬性中指定的任何值。  
  
-   停用與 DirectQuery 模式不相容的設計功能。  
  
-   驗證現有的模型。  
  
 此程序描述如何在設計工具中啟用 DirectQuery 模式。  
  
### <a name="to-enable-use-of-directquery-in-a-model"></a>若要在模型中啟用 DirectQuery  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟方案檔。  
  
2.  在 [物件總管] 中，按兩下 Model.bim 檔案。  
  
3.  在 [**屬性**] 窗格中，將屬性**DirectQueryMode**變更為**On**。  
  
4.  如果發生錯誤，請在 Visual Studio 中開啟**錯誤清單**，並解決會導致模型無法切換至 DirectQuery 模式的任何問題。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的 DirectQuery 模式](directquery-mode-ssas-tabular.md)  
  
  
