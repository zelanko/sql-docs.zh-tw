---
title: 以路徑連接元件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], connections
- components [Integration Services], connections
- connections [Integration Services], data flow components
ms.assetid: 05633e4c-1370-4b05-802b-f36b07dd71c8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 776e3d8c8b8731fb56d51213ffe085c857066cd7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62834020"
---
# <a name="connect-components-with-paths"></a>以路徑連接元件
  您可以在 **設計師中** [資料流程] [!INCLUDE[ssIS](../includes/ssis-md.md)] 索引標籤的設計介面上，建構封裝中的資料流程。 如果資料流程包含兩個資料流程元件，將來源或轉換的輸出連接到轉換或目的地的輸入，便可以連接這兩個元件。 兩個資料流程元件之間的連接子稱為路徑。  
  
 下圖顯示的範例資料流程中，包含一個來源元件、兩個轉換、一個目的地元件，以及連接元件的路徑。  
  
 ![Data flow](media/mw-dts-08.gif "Data flow")  
  
 在連接兩個元件之後，您可以在 **[資料流程路徑編輯器]** 中，檢視經由路徑移動的資料之中繼資料，以及路徑的屬性。 如需詳細資訊，請參閱 [Integration Services Paths](data-flow/integration-services-paths.md)。  
  
 您也可以將資料檢視器加入路徑。 資料檢視器可讓您在封裝執行時，檢視在資料流程元件之間移動的資料。  
  
### <a name="to-connect-components-in-a-data-flow"></a>連接資料流程中的元件  
  
-   [連接資料流程中的元件](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-path-properties"></a>設定路徑屬性  
  
-   [使用資料流程路徑編輯器來設定路徑的屬性](../../2014/integration-services/set-the-properties-of-a-path-by-using-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>若要檢視路徑中繼資料  
  
-   [在資料流程路徑編輯器中檢視路徑中繼資料](../../2014/integration-services/view-path-metadata-in-the-data-flow-path-editor.md)  
  
### <a name="to-view-path-metadata"></a>若要檢視路徑中繼資料  
  
-   [將資料檢視器新增到資料流程](../../2014/integration-services/add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料流程工作](control-flow/data-flow-task.md)   
 [資料流程](data-flow/data-flow.md)   
 [使用轉換來轉換資料](data-flow/transformations/transform-data-with-transformations.md)   
 [資料中的錯誤處理](data-flow/error-handling-in-data.md)  
  
  
