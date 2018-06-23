---
title: 檢視套件物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0128e5236f517ba9d466f8517145fa44170d0657
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146554"
---
# <a name="view-package-objects"></a>檢視封裝物件
  在「[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」中，[封裝總管] 索引標籤提供封裝的總管檢視。 此檢視反映 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 架構的容器階層。 封裝容器位於階層的頂端，您可以展開封裝以檢視其中的連接、可執行檔、事件處理常式、記錄提供者、優先順序條件約束和變數。  
  
 可執行檔 (封裝中的容器和工作) 可包含事件處理常式、優先順序條件約束和變數。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支援容器的巢狀階層，而「For 迴圈」、「Foreach 迴圈」和「時序」容器可包含其他可執行檔。  
  
 如果某個封裝包含資料流程，封裝總管會列出「資料流程」工作，並包含一個列出資料流程元件的 [元件] 資料夾。  
  
 藉由 [封裝總管] 索引標籤，您可以刪除封裝中的物件並存取 [屬性] 視窗以檢視物件屬性。  
  
 下圖顯示簡單封裝的樹狀檢視。  
  
 ![[套件總管] 索引標籤的螢幕擷取畫面](media/packageexplorer.gif "[套件總管] 索引標籤的螢幕擷取畫面")  
  
### <a name="to-view-package-content"></a>檢視封裝內容  
  
-   [在 [封裝總管] 中檢視封裝物件](../../2014/integration-services/view-package-objects-in-package-explorer.md)  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [Integration Services 容器](control-flow/integration-services-containers.md)   
 [優先順序條件約束](control-flow/precedence-constraints.md)   
 [Integration Services &#40;SSIS&#41;變數](integration-services-ssis-variables.md)   
 [Integration Services &#40;SSIS&#41; 事件處理常式](integration-services-ssis-event-handlers.md)   
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)  
  
  