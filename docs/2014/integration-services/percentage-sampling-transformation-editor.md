---
title: 百分比取樣轉換編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- Percentage Sampling Transformation Editor
ms.assetid: 2c40d804-26a3-4d35-809b-bc923d83d451
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1734dd95a0744e08e57bcdff3a80f882b926c2ba
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964689"
---
# <a name="percentage-sampling-transformation-editor"></a>百分比取樣轉換編輯器
  使用 **[百分比取樣轉換編輯器]** 對話方塊，即可依指定的資料列百分比，將輸入的一部分分割為取樣。 這個轉換會將輸入分成兩個不同的輸出。  
  
 若要深入了解百分比取樣轉換，請參閱＜ [Percentage Sampling Transformation](data-flow/transformations/percentage-sampling-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **資料列的百分比**  
 指定在輸入中，要作為取樣的資料列百分比。  
  
 此屬性的值可以使用屬性運算式指定。  
  
 **取樣輸出名稱**  
 提供包含取樣資料列之輸出的唯一名稱。 提供的名稱將顯示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師內。  
  
 **未選取的輸出名稱**  
 提供輸出的唯一名稱，其中包含從取樣排除的資料列。 提供的名稱將顯示在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師內。  
  
 **使用下列隨機種子**  
 指定轉換用來建立取樣之隨機號碼產生器的取樣種子。 只建議用於開發和測試。 如果未指定隨機種子，轉換會使用 Microsoft Windows 滴答計數。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [資料列取樣轉換](data-flow/transformations/row-sampling-transformation.md)  
  
  
