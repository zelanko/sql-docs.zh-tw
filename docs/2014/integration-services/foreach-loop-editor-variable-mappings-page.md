---
title: Foreach 迴圈編輯器 （變數對應頁面） |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.mapping.f1
ms.assetid: aa847b87-f391-48a5-9849-eeda2d6b00b9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3fc54d5b287cd71ba303d34693e815c07b9cc3b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068071"
---
# <a name="foreach-loop-editor-variable-mappings-page"></a>Foreach 迴圈編輯器 (變數對應頁面)
  使用 [Foreach 迴圈編輯器] 對話方塊的 [變數對應] 頁面，即可將變數對應至集合值。 會用迴圈之每個反覆運算上的集合值來更新變數的值。  
  
 若要了解如何在 Integration Services 封裝中使用「Foreach 迴圈」容器，請參閱 [Foreach 迴圈容器](control-flow/foreach-loop-container.md) 。 若要了解如何設定此容器，請參閱 [設定 Foreach 迴圈容器](../../2014/integration-services/configure-a-foreach-loop-container.md)。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教學課程中的＜建立簡易 ETL 封裝教學課程＞包含了一門教您加入和設定「Foreach 迴圈」的課程。  
  
## <a name="options"></a>選項。  
 **變數**  
 選取現有的變數，或按一下 [\<新增變數...>] 以建立新的變數。  
  
> [!NOTE]  
>  對應變數之後，新資料列會自動加入 [變數] 清單。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)、[加入變數](../../2014/integration-services/add-variable.md)  
  
 **Index**  
 如果使用 Foreach 項目列舉值，請指定集合值中要對應至變數的資料行索引。 針對其他列舉值類型，此索引是唯讀的。  
  
> [!NOTE]  
>  索引是以 0 為基底。  
  
 **相關主題**:[循環使用 Excel 檔案和使用 「 Foreach 迴圈 」 容器的資料表](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
 **刪除**  
 選取變數，然後按一下 [刪除]。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Foreach 迴圈編輯器&#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [Foreach 迴圈編輯器&#40;的集合頁面&#41;](../../2014/integration-services/foreach-loop-editor-collection-page.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [For 迴圈容器](control-flow/for-loop-container.md)  
  
  
