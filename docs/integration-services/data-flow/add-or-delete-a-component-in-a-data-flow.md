---
title: "在資料流程中新增或刪除元件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding components
- components [Integration Services], data flow
ms.assetid: d99124f9-0994-4f40-a48e-fdca6a4383e7
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2a061024c6921bdc2feccc9c6372104b4a4c70e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="add-or-delete-a-component-in-a-data-flow"></a>在資料流程中加入或刪除元件
  資料流程元件指資料流程中的來源、目的地和轉換。 封裝中的控制流程必須包含「資料流程」工作，您才能將元件加入到資料流程中。  
  
 下列程序將描述如何在封裝的資料流程中加入或刪除元件。  
  
### <a name="to-add-a-component-to-a-data-flow"></a>將元件加入資料流程  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程] 索引標籤，然後按兩下包含要加入元件之資料流程的「資料流程」工作。  
  
4.  在 [工具箱] 中，展開 [資料流程來源]、[資料流程轉換] 或 [資料流程目的地]，然後將資料流程項目拖曳到 [資料流程] 索引標籤的設計介面上。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-delete-a-component-from-a-data-flow"></a>從資料流程中刪除元件  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [控制流程] 索引標籤，然後按兩下包含您要刪除元件之資料流程的「資料流程」工作。  
  
4.  以滑鼠右鍵按一下資料流程元件，然後按一下 [刪除]。  
  
5.  確認刪除作業。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [連接資料流程中的元件](../../integration-services/data-flow/connect-components-in-a-data-flow.md)   
 [偵錯資料流程](../../integration-services/troubleshooting/debugging-data-flow.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
