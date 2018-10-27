---
title: 鎖定和解除鎖定資料庫 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
ms.openlocfilehash: e1f518f846a6e0bb87f858d7a5798eb9a7e9c8d0
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146273"
---
# <a name="locking-and-unlocking-databases-xmla"></a>鎖定和解除鎖定資料庫 (XMLA)
  您可以鎖定及解除鎖定資料庫分別使用，則[鎖定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)並[解除鎖定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)XML for Analysis (XMLA) 中的命令。 一般而言，其他 XMLA 命令會視需要自動鎖定和解除鎖定物件，以便在執行期間完成命令。 您可以明確地鎖定或解除鎖定資料庫來執行單一交易內的多個命令，例如[批次](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令，以防止其他應用程式資料庫將寫入交易認可。  
  
## <a name="locking-databases"></a>鎖定資料庫  
 `Lock` 命令會在目前使用中交易的內容中鎖定某個物件，以便共用或獨佔使用。 鎖定物件會防止認可交易，直到移除鎖定為止。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援兩種類型的鎖定，共用的鎖定和獨佔鎖定。 如需所支援的鎖定類型[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，請參閱 <<c2> [ 模式項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla)。</c2>  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 僅允許鎖定資料庫。 [物件](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)項目必須包含的物件參考[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫。 如果您沒有指定 `Object` 元素或者 `Object` 元素參考資料庫以外的物件，就會發生錯誤。  
  
> [!IMPORTANT]  
>  只有資料庫管理員或伺服器管理員可以明確發出 `Lock` 命令。  
  
 其他命令會隱含地針對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫發出 `Lock` 命令。 從資料庫，例如任何讀取資料或中繼資料的任何作業[Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法或[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法執行[陳述式](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令都會隱含地發出共用在資料庫上的鎖定。 任何認可的交易，變更資料或中繼資料物件上[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫，例如`Execute`方法執行[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令都會隱含地發出資料庫的獨佔鎖定。  
  
## <a name="unlocking-objects"></a>解除鎖定物件  
 `Unlock` 命令會移除在目前使用中交易內容內部建立的鎖定。  
  
> [!IMPORTANT]  
>  只有資料庫管理員或伺服器管理員可以明確發出 `Unlock` 命令。  
  
 所有鎖定都會保存在目前交易的內容中。 當目前的交易經過認可或回復時，就會自動釋放在交易內部定義的所有鎖定。  
  
## <a name="see-also"></a>另請參閱  
 [鎖定項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Unlock 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
