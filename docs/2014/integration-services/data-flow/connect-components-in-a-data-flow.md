---
title: 連接資料流程中的元件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd6904980e160b027147649751d076085307a3ec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204458"
---
# <a name="connect-components-in-a-data-flow"></a>連接資料流程中的元件
  此程序描述如何將資料流程中的元件輸出，連接到同一資料流程中的其他元件。  
  
### <a name="to-connect-components-in-a-data-flow"></a>連接資料流程中的元件  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程] 索引標籤，然後按兩下包含您要在其中連接元件之資料流程的「資料流程」工作。  
  
4.  在 [資料流程] 索引標籤的設計介面上，選取您要連接的轉換或來源。  
  
5.  將轉換或來源的綠色輸出箭頭拖曳至另一轉換或目的地。 某些資料流程元件有錯誤輸出，您可以使用相同方式加以連接。  
  
    > [!NOTE]  
    >  某些資料流程元件具有多個輸出，您可以將每個輸出連接到另一個轉換或目的地。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [加入或刪除資料流中的元件](data-flow.md)   
 [資料流程元件中設定錯誤輸出](../configure-an-error-output-in-a-data-flow-component.md)   
 [資料流程](data-flow.md)  
  
  
