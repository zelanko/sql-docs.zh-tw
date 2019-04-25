---
title: OData 來源編輯器 （連接頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- Sql12.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 85ac46b918918f7e9dac715e11909ffeb9c46a29
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767140"
---
# <a name="odata-source-editor-connection-page"></a>OData 來源編輯器 (連接頁面)
  使用 **[OData 來源編輯器]** 對話方塊的 **[連接]** 頁面，選取 OData 來源的 OData 連接管理員。 此頁面也可讓您指定集合或資源路徑及任何查詢選項，以指示需要從 OData 來源擷取哪些資料。 若要深入了解 OData 來源，請參閱＜ [OData Source](data-flow/odata-source.md)＞。  
  
## <a name="static-options"></a>靜態選項  
 **OData 連接管理員**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [OData 連線管理員編輯器] 對話方塊建立新的連線管理員。  
  
 **使用集合或資源路徑**  
 從來源中指定選取資料的方法。  
  
|選項|描述|  
|------------|-----------------|  
|Collection|使用集合名稱從 OData 來源擷取資料。|  
|資源路徑|使用資源路徑從 OData 來源擷取資料。|  
  
 **查詢選項**  
 指定查詢的選項。  例如：$top=5  
  
 **摘要 url**  
 根據您在此對話方塊中選取的選項顯示唯讀摘要 URL。  
  
 **預覽**  
 使用 [預覽] 對話方塊來預覽結果。 **[預覽]** 最多可顯示 20 個資料列。  
  
## <a name="dynamic-options"></a>動態選項  
  
### <a name="use-collection-or-resource-path--collection"></a>使用集合或資源路徑 = 集合  
 **Collection**  
 從下拉式清單中選取集合。  
  
### <a name="use-collection-or-resource-path--resource-path"></a>使用集合或資源路徑 = 資源路徑  
 **Resource path**  
 輸入資源路徑。 例如：Employees  
  
## <a name="see-also"></a>另請參閱  
 [OData 來源編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/odata-source-editor-columns-page.md)   
 [OData 來源編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/odata-source-editor-error-output-page.md)   
 [OData Connection Manager](connection-manager/odata-connection-manager.md)  
  
  
