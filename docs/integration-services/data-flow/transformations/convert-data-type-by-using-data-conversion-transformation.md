---
title: 使用資料轉換轉換資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b7494eb9879c8ceb5e80e28b071d4ae6817bf75
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283112"
---
# <a name="convert-data-type-by-using-data-conversion-transformation"></a>使用資料轉換轉換資料類型
  若要加入及設定「資料轉換」，封裝必須已包含至少一個「資料流程」工作及一個來源。  
  
### <a name="to-convert-data-to-a-different-data-type"></a>轉換資料至不同的資料類型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後將 [資料轉換] 從 **[工具箱]** 拖曳到設計介面。  
  
4.  將連接子從來源或前一轉換拖曳至 [資料轉換]，以便將 [資料轉換] 連接到資料流程。  
  
5.  按兩下 [資料轉換]。  
  
6.  在 [資料轉換編輯器] 對話方塊中，於 [可用的輸入資料行] 資料表中，選取您要轉換其資料類型之資料行旁邊的核取方塊。  
  
    > [!NOTE]  
    >  您可以對輸入資料行套用多個資料轉換。  
  
7.  (選擇性) 修改 **[輸出別名]** 資料行中的預設值。  
  
8.  在 **[資料類型]** 清單中，選取資料行的新資料類型。 預設資料類型是輸入資料行的資料類型。  
  
9. (選擇性) 視所選取資料類型而定，更新 **[長度]**、 **[有效位數]**、 **[小數位數]** 及 **[字碼頁]** 資料行中的值。  
  
10. 若要設定錯誤輸出，請按一下 **[設定錯誤輸出]**。 如需詳細資訊，請參閱 [偵錯資料流程](../../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
11. 按一下 [確定] 。  
  
12. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../../integration-services/data-flow/integration-services-paths.md)   
 [Integration Services 資料類型](../../../integration-services/data-flow/integration-services-data-types.md)   
 [資料流程工作](../../../integration-services/control-flow/data-flow-task.md)  
  
  
