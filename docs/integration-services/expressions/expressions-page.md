---
title: 運算式頁面 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2fc767224bb77f3ddbb0f6f562a5d5fce2a56981
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270864"
---
# <a name="expressions-page"></a>運算式頁面
  使用 [運算式] 頁面，即可編輯屬性運算式，並存取 [屬性運算式編輯器] 和 [屬性運算式產生器] 對話方塊。  
  
 屬性運算式會在執行封裝時更新屬性值。 屬性運算式可與封裝、工作、容器、連接管理員以及一些資料流程元件的屬性一起使用。 會評估這些運算式並使用其結果，但不會使用您在設定封裝和封裝物件時所設定的屬性值。 運算式可以包含變數以及運算式語言提供的函數與運算子。 例如，您可以將包含字串 "Weather forecast for " 的變數值與 GETDATE() 函數的傳回結果，串連成字串 "Weather forecast for 4/5/2006"，以產生「傳送郵件」工作的主旨列。  
  
 若要深入了解撰寫運算式以及使用屬性運算式，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md) 和 [在封裝中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
## <a name="options"></a>選項。  
 **運算式 (...)**  
 按一下省略符號，即可開啟 **屬性運算式編輯器** 對話方塊。 如需詳細資訊，請參閱 [屬性運算式編輯器](../../integration-services/expressions/property-expressions-editor.md)。  
  
 **\<屬性名稱>**  
 按一下省略符號，即可開啟 **[運算式產生器]** 對話方塊。 如需詳細資訊，請參閱 [Expression Builder](../../integration-services/expressions/expression-builder.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)   
 [系統變數](../../integration-services/system-variables.md)   
 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
