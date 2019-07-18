---
title: 模糊群組轉換編輯器 （連接管理員索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.connection.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 47b1446d-5331-473c-9cb5-a98b1f55bf5f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7cfee2c2a79410d73eb6ca4da47f0fd361a24fb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058334"
---
# <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>模糊群組轉換編輯器 (連接管理員索引標籤)
  使用 **[模糊群組轉換編輯器]** 對話方塊的 **[連接管理員]** 索引標籤，來選取現有的連接或建立新的連接。  
  
> [!NOTE]  
>  連接所指定的伺服器必須正在執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 模糊群組轉換會在 tempdb 中建立暫存資料物件，而這個物件可能會與轉換的完整輸出一樣大。 當轉換執行時，它會對這些暫存物件發出伺服器查詢。 這樣會影響伺服器的整體效能。  
  
 若要深入了解模糊群組轉換，請參閱＜ [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md)＞。  
  
## <a name="options"></a>選項  
 **[無快取]**  
 使用清單方塊來選取現有的 OLE DB 連接管理員，或使用 [新增]  按鈕來建立新的連接。  
  
 **新增**  
 使用 [設定 OLE DB 連接管理員]  對話方塊來建立新的連接。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用模糊群組轉換來識別相似的資料列](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
