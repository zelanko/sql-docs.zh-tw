---
title: 鎖定和解除鎖定資料庫（XMLA） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 290f1e5fe7efb876ab6c24004c7465cf109de0d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702226"
---
# <a name="locking-and-unlocking-databases-xmla"></a>鎖定和解除鎖定資料庫 (XMLA)
  您可以使用 XML for Analysis （XMLA）中的 [[鎖定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)] 和 [[解除鎖定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)] 命令，分別鎖定和解除鎖定資料庫。 一般而言，其他 XMLA 命令會視需要自動鎖定和解除鎖定物件，以便在執行期間完成命令。 您可以明確地鎖定或解除鎖定資料庫，以便在單一交易中執行多個命令，例如[批次](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令，同時防止其他應用程式將寫入交易認可到資料庫。  
  
## <a name="locking-databases"></a>鎖定資料庫  
 
  `Lock` 命令會在目前使用中交易的內容中鎖定某個物件，以便共用或獨佔使用。 鎖定物件會防止認可交易，直到移除鎖定為止。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援兩種鎖定類型：共用鎖定和獨佔鎖定。 如需所支援之鎖定類型的詳細[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資訊，請參閱[MODE 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla)。  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 僅允許鎖定資料庫。 [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)元素必須包含[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫的物件參考。 如果您沒有指定 `Object` 元素或者 `Object` 元素參考資料庫以外的物件，就會發生錯誤。  
  
> [!IMPORTANT]  
>  只有資料庫管理員或伺服器管理員可以明確發出 `Lock` 命令。  
  
 其他命令會隱含地針對 `Lock` 資料庫發出 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 命令。 任何從資料庫讀取資料或中繼資料的作業（例如任何[探索](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法或執行[語句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令的[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法）都會隱含地發出資料庫的共用鎖定。 任何將資料或中繼資料變更認可至[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫上之物件的交易（例如，執行`Execute` [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令的方法）都會隱含地發出資料庫的獨佔鎖定。  
  
## <a name="unlocking-objects"></a>解除鎖定物件  
 
  `Unlock` 命令會移除在目前使用中交易內容內部建立的鎖定。  
  
> [!IMPORTANT]  
>  只有資料庫管理員或伺服器管理員可以明確發出 `Unlock` 命令。  
  
 所有鎖定都會保存在目前交易的內容中。 當目前的交易經過認可或回復時，就會自動釋放在交易內部定義的所有鎖定。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XMLA&#41;的 Lock 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [&#40;XMLA&#41;解除鎖定元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
