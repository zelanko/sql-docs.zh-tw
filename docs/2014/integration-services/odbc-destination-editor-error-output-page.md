---
title: ODBC 目的地編輯器 （錯誤輸出頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: 0a743f8d-2a51-4296-9976-8104f5ca22d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 972357372fe6d0281aedb57d49dd8d50682085b5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057194"
---
# <a name="odbc-destination-editor-error-output-page"></a>ODBC 目的地編輯器 (錯誤輸出頁面)
  使用 **[ODBC 目的地編輯器]** 對話方塊的 **[錯誤輸出]** 頁面，即可選取錯誤處理選項。  
  
 若要了解有關 ODBC 目的地的詳細資訊，請參閱＜ [ODBC Destination](data-flow/odbc-destination.md)＞。  
  
 **若要開啟 ODBC 目的地編輯器的錯誤輸出頁面**  
  
## <a name="task-list"></a>工作清單  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 目的地的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程] 索引標籤中，按兩下 ODBC 目的地。  
  
-   在 **[ODBC 目的地編輯器]** 中，按一下 **[錯誤輸出]**。  
  
## <a name="options"></a>選項  
  
### <a name="inputoutput"></a>輸入/輸出  
 檢視資料來源的名稱。  
  
### <a name="column"></a>「資料行」  
 未使用。  
  
### <a name="error"></a>錯誤  
 選取 ODBC 目的地應該如何處理流程中的錯誤：忽略失敗、重新導向資料列，或使元件失效。  
  
### <a name="truncation"></a>截斷  
 選取 ODBC 目的地應該如何處理流程中的截斷：忽略失敗、重新導向資料列，或使元件失效。  
  
### <a name="description"></a>描述  
 檢視錯誤的描述。  
  
### <a name="set-this-value-to-selected-cells"></a>將這個值設定到選取的資料格  
 選取發生錯誤或截斷時 ODBC 目的地如何處理所有選取的資料格：忽略失敗、重新導向資料列，或使元件失效。  
  
### <a name="apply"></a>套用  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="error-handling-options"></a>錯誤處理選項  
 您可以使用下列選項來設定 ODBC 目的地處理錯誤和截斷的方式。  
  
### <a name="fail-component"></a>失敗元件  
 當發生錯誤或截斷時，資料流程工作將失敗。 這是預設行為。  
  
### <a name="ignore-failure"></a>忽略失敗  
 忽略錯誤或截斷。  
  
### <a name="redirect-flow"></a>重新導向流程  
 導致錯誤或截斷的資料列會導向至 ODBC 目的地的錯誤輸出。 如需詳細資訊，請參閱＜ODBC 目的地＞。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 目的地編輯器 &#40;連線管理員頁面&#41;](../../2014/integration-services/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 目的地編輯器 &#40;對應頁面&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)  
  
  
