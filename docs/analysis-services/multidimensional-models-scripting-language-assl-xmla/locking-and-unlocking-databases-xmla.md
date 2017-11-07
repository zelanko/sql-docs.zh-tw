---
title: "鎖定和解除鎖定資料庫 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8924b6a21a0bb815ec377072615db2efb4fa2f07
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="locking-and-unlocking-databases-xmla"></a>鎖定和解除鎖定資料庫 (XMLA)
  您可以鎖定與解除鎖定資料庫分別使用、[鎖定](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)和[解除鎖定](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)XML for Analysis (XMLA) 中的命令。 一般而言，其他 XMLA 命令會視需要自動鎖定和解除鎖定物件，以便在執行期間完成命令。 您可以明確地鎖定或解除鎖定資料庫，執行單一交易內的多個命令，例如[批次](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令，以防止其他應用程式資料庫將寫入交易認可。  
  
## <a name="locking-databases"></a>鎖定資料庫  
 **鎖定**命令會鎖定物件，以便共用或獨佔使用，目前使用中交易內容中。 鎖定物件會防止認可交易，直到移除鎖定為止。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支援兩種類型的鎖定，共用的鎖定和獨佔鎖定。 如需有關所支援的鎖定類型[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，請參閱[Mode 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 僅允許鎖定資料庫。 [物件](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)元素必須包含的物件參考[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 如果**物件**未指定項目或**物件**元素參考資料庫以外的物件發生錯誤。  
  
> [!IMPORTANT]  
>  只有資料庫管理員或伺服器管理員可以明確發出**鎖定**命令。  
  
 其他命令會隱含地問題**鎖定**命令[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 讀取資料庫，例如任何資料或中繼資料的任何作業[探索](../../analysis-services/xmla/xml-elements-methods-discover.md)方法或[Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)方法執行[陳述式](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)命令都會隱含地發出共用在資料庫上的鎖定。 在將資料或中繼資料的變更認可至物件的任何交易[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫，例如**Execute**方法執行[Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令，以隱含方式上發出獨佔鎖定資料庫。  
  
## <a name="unlocking-objects"></a>解除鎖定物件  
 **Unlock** 命令會移除在目前使用中交易內容內部建立的鎖定。  
  
> [!IMPORTANT]  
>  只有資料庫管理員或伺服器管理員可以明確發出 **Unlock** 命令。  
  
 所有鎖定都會保存在目前交易的內容中。 當目前的交易經過認可或回復時，就會自動釋放在交易內部定義的所有鎖定。  
  
## <a name="see-also"></a>另請參閱  
 [Lock 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)   
 [解除鎖定元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [使用 Analysis Services 中的 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

