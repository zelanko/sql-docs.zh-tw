---
title: 查閱轉換編輯器 （錯誤輸出頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.erroroutput.f1
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c9d2417c844998547480a2f03f6dcf9409ff7656
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388086"
---
# <a name="lookup-transformation-editor-error-output-page"></a>查閱轉換編輯器 (錯誤輸出頁面)
  使用 **[查閱轉換編輯器]** 對話方塊的 **[錯誤輸出]** 頁面，來指定錯誤處理選項。  
  
 若要深入了解查閱轉換，請參閱＜ [Lookup Transformation](data-flow/transformations/lookup-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **輸入/輸出**  
 檢視輸入的名稱。  
  
 **資料行**  
 未使用。  
  
 **錯誤**  
 指定處理在參考資料集中沒有相符項目的資料列時會發生什麼類型的錯誤：  
  
-   忽略失敗並將資料列導向輸出。  
  
-   將資料列重新導向錯誤輸出。  
  
-   使元件失效。  
  
 在 **[指定如何處理無相符項目的資料列]** 清單中選取 **[將資料列重新導向無相符結果輸出]** 時，無法使用此選項。 此清單位在 **[查閱轉換編輯器]** 對話方塊的 **[一般]** 頁面上。  
  
 **相關主題：**[資料中的錯誤處理](data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定資料截斷發生時要採取的動作：  
  
-   忽略失敗。  
  
-   重新導向資料列。  
  
-   使元件失效。  
  
 **說明**  
 檢視作業的描述。  
  
 **將選取的資料格設定為此值**  
 指定在錯誤或截斷發生時對所有選取的資料格進行什麼作業。  
  
-   忽略失敗。  
  
-   重新導向資料列。  
  
-   使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
