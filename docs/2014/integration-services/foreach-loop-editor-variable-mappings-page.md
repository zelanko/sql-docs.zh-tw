---
title: Foreach 迴圈編輯器（變數對應頁面） |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.mapping.f1
ms.assetid: aa847b87-f391-48a5-9849-eeda2d6b00b9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 043077496e1ec1a1cad147725d7f722364f6a54c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425495"
---
# <a name="foreach-loop-editor-variable-mappings-page"></a>Foreach 迴圈編輯器 (變數對應頁面)
  使用 [Foreach 迴圈編輯器]**** 對話方塊的 [變數對應]**** 頁面，即可將變數對應至集合值。 會用迴圈之每個反覆運算上的集合值來更新變數的值。  
  
 若要了解如何在 Integration Services 封裝中使用「Foreach 迴圈」容器，請參閱 [Foreach 迴圈容器](control-flow/foreach-loop-container.md) 。 若要了解如何設定此容器，請參閱 [設定 Foreach 迴圈容器](../../2014/integration-services/configure-a-foreach-loop-container.md)。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建立簡單的 ETL 封裝教學課程中，包含一個教您加入和設定 Foreach 迴圈的課程。  
  
## <a name="options"></a>選項  
 **變**  
 選取現有的變數，或按一下 \<**New variable...**> 以建立新的變數。  
  
> [!NOTE]  
>  對應變數之後，新資料列會自動加入 [變數]**** 清單。  
  
 **相關主題**： [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[新增變數](../../2014/integration-services/add-variable.md)  
  
 **索引**  
 如果使用 Foreach 項目列舉值，請指定集合值中要對應至變數的資料行索引。 針對其他列舉值類型，此索引是唯讀的。  
  
> [!NOTE]  
>  索引是以 0 為基底。  
  
 **相關主題**： [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
 **刪除**  
 選取變數，然後按一下 [刪除]****。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[Foreach 迴圈編輯器] &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [[Foreach 迴圈編輯器] &#40;集合] 頁面&#41;](../../2014/integration-services/foreach-loop-editor-collection-page.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [For 迴圈容器](control-flow/for-loop-container.md)  
  
  
