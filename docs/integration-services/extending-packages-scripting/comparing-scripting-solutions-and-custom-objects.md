---
title: 比較指令碼解決方案和自訂物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba27959fa5c98b26bd6dc4fdf60d695829c7382d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653445"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>比較指令碼方案和自訂物件
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 指令碼工作或是指令碼元件可以實作許多可能會應用於自訂 Managed 工作或資料流程元件的相同功能。 以下是可協助您針對需求選擇適當類型之工作的一些考量：  
  
-   如果組態或功能是個別封裝特有的，您應該使用指令碼工作或指令碼元件，而不是開發自訂物件。  
  
-   如果功能是一般性的，而且未來可能用於其他封裝或是由其他開發人員使用，您應該建立自訂物件，而不是使用指令碼方案。 您可以在任何封裝中使用自訂物件，然而指令碼只能在建立它的封裝中使用。  
  
-   如果程式碼將在相同的封裝中重複使用，您應該考慮建立自訂物件。 將程式碼從某個指令碼工作或元件複製到其他指令碼工作或元件，將會降低可維護性，因為這將使得維護和更新程式碼的多個複本更加困難。  
  
-   如果實作在一段時間後將會變更，請考慮使用自訂物件。 自訂物件可以和父封裝分開開發和部署，然而對指令碼方案的更新則需要重新部署整個封裝。  
  
## <a name="see-also"></a>另請參閱  
 [使用自訂物件擴充封裝](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
