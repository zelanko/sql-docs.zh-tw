---
title: ODBC 來源編輯器 （資料行頁面） |Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c81948bfcb6d0c2c523d563e850e9466ae45679a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135202"
---
# <a name="odbc-source-editor-columns-page"></a>ODBC 來源編輯器 (資料行頁面)
  使用 [ODBC 來源編輯器] 對話方塊的 [資料行] 頁面，即可將輸出資料行對應至每個外部 (來源) 資料行。  
  
 若要了解有關 ODBC 來源的詳細資訊，請參閱＜ [ODBC Source](data-flow/odbc-source.md)＞。  
  
## <a name="task-list"></a>工作清單  
 **若要開啟 ODBC 來源編輯器的資料行頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 來源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 ODBC 來源。  
  
3.  在 **[ODBC 來源編輯器]** 中，按一下 **[資料行]**。  
  
## <a name="options"></a>選項。  
  
### <a name="available-external-columns"></a>可用的外部資料行  
 資料來源中可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。 請從來源選取要使用的資料行。 選取的資料行就會依照選取的順序加入至 **[外部資料行]** 清單。  
  
 選取 **[全選]** 核取方塊，即可選取所有資料行。  
  
### <a name="external-column"></a>外部資料行  
 外部 (來源) 資料行的檢視，這些資料行會依照您在設定取用 ODBC 來源資料之元件時所看見的順序列出。  
  
### <a name="output-column"></a>輸出資料行  
 為每個輸出資料行輸入唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。 輸入的名稱就會顯示在 SSIS 設計師中。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 來源編輯器&#40;連接管理員頁面&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [ODBC 來源編輯器&#40;錯誤輸出頁面&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  