---
title: 比較指令碼解決方案和自訂物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1034c021c35efa7c7fb7c6a7090f61c848aa224e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895007"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>比較指令碼方案和自訂物件
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 指令碼工作或是指令碼元件可以實作許多可能會應用於自訂 Managed 工作或資料流程元件的相同功能。 以下是可協助您針對需求選擇適當類型之工作的一些考量：  
  
-   如果組態或功能是個別封裝特有的，您應該使用指令碼工作或指令碼元件，而不是開發自訂物件。  
  
-   如果功能是一般性的，而且未來可能用於其他封裝或是由其他開發人員使用，您應該建立自訂物件，而不是使用指令碼方案。 您可以在任何封裝中使用自訂物件，然而指令碼只能在建立它的封裝中使用。  
  
-   如果程式碼將在相同的封裝中重複使用，您應該考慮建立自訂物件。 將程式碼從某個指令碼工作或元件複製到其他指令碼工作或元件，將會降低可維護性，因為這將使得維護和更新程式碼的多個複本更加困難。  
  
-   如果實作在一段時間後將會變更，請考慮使用自訂物件。 自訂物件可以和父封裝分開開發和部署，然而對指令碼方案的更新則需要重新部署整個封裝。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [使用自訂物件擴充封裝](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
