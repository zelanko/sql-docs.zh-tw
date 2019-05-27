---
title: 查閱轉換編輯器 （一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.general.f1
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb83e95bd13b566f46386cf10676ee882a954762
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057835"
---
# <a name="lookup-transformation-editor-general-page"></a>查閱轉換編輯器 (一般頁面)
  使用 [查閱轉換編輯器] 對話方塊的 **[一般]** 頁面來選取快取模式、選取連接類型，及指定如何處理無相符項目的資料列。  
  
 若要深入了解查閱轉換，請參閱＜ [Lookup Transformation](data-flow/transformations/lookup-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **完整快取**  
 在查閱轉換執行之前產生參考資料集並將其載入快取。  
  
 **部分快取**  
 在查閱轉換執行期間產生參考資料集。 將參考資料集中具有相符項目的資料列，以及在資料集中沒有相符項目的資料列載入到快取。  
  
 **沒有快取**  
 在查閱轉換執行期間產生參考資料集。 沒有資料會載入到快取。  
  
 **快取連接管理員**  
 將查閱轉換設定為使用快取連接管理員。 只有在選取 [完整快取] 選項時，才能使用這個選項。  
  
 **[無快取]**  
 將查閱轉換設定為使用 OLE DB 連接管理員。  
  
 **指定如何處理無相符項目的資料列**  
 選取選項以處理沒有至少符合參考資料集中一個項目的資料列。  
  
 當您選取 **[將資料列重新導向無相符結果輸出]** 時，資料列會重新導向無相符結果輸出，且不當做錯誤處理。 無法使用 **[查閱轉換編輯器]** 對話方塊的 **[錯誤輸出]** 頁面上的 **[錯誤]** 選項。  
  
 從 **[指定如何處理無相符項目的資料列]** 清單方塊中選取任何其他選項時，會將資料列當做錯誤處理。 可以使用 **[錯誤輸出]** 頁面上的 **[錯誤]** 選項。  
  
## <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章： [查閱快取模式](https://go.microsoft.com/fwlink/?LinkId=219518)   
  
## <a name="see-also"></a>另請參閱  
 [Cache Connection Manager](connection-manager/cache-connection-manager.md)   
 [查閱轉換編輯器 &#40;連接頁面&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [查閱轉換編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [查閱轉換編輯器 &#40;進階頁面&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)  
  
  
