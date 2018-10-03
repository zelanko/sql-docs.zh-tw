---
title: 在 維度設計師中檢視屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e7e5ea7af394905d9f5efcb27dce4d102fb5d3c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180038"
---
# <a name="view-attributes-in-dimension-designer"></a>在維度設計師中檢視屬性
  屬性是在維度物件上建立的。 您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的維度設計師，檢視和設定屬性。 維度設計師之 [維度結構] 索引標籤的 [屬性] 窗格，會列出維度中的屬性。 使用此窗格，即可加入、移除或設定屬性。 您也可以選取屬性，以用來做為新階層中的層級，或者加入做為現有階層的層級。  
  
 若要檢視維度中的屬性，請針對維度開啟維度設計師。 設計師之 [維度結構] 索引標籤的 [屬性] 窗格，會顯示維度中的屬性。 您可以藉由指向清單、 樹狀或方格檢視之間切換**顯示屬性於**上**維度**功能表[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，然後按一下其中一個下表所示的命令。  
  
|顯示屬性於|描述|  
|------------------------|-----------------|  
|**清單**|以清單格式顯示屬性。<br /><br /> 以滑鼠右鍵按一下某個屬性，即可將屬性從清單中刪除、將屬性重新命名，或者變更屬性的使用方式。<br /><br /> 使用此檢視建立階層。 屬性 (Attribute) 資訊和成員屬性 (Property) 是看不到的。|  
|**樹狀結構**|以樹狀格式顯示屬性，且維度是樹狀中的最上層節點。 使用此檢視，即可檢視和建立成員屬性。 也您可以使用此檢視來建立階層。 執行下列動作，即可展開屬性來檢視其屬性關聯性，或是建立新的屬性關聯性：<br /><br /> 按一下維度、屬性 (Attribute) 或成員屬性 (Property)，即可在 [屬性] (Property) 視窗中檢視其屬性 (Property)。<br /><br /> 以滑鼠右鍵按一下屬性 (Attribute) 或成員屬性 (Property)，即可從清單刪除屬性、將屬性重新命名，或者變更屬性的使用方式。|  
|**方格**|以方格格式顯示屬性。 按一下方格中的任一個資料列，即可檢視該屬性 (Attribute) 的屬性 (Property)。  使用此檢視來建立和設定屬性。 方格會顯示下列資料行：<br /><br /> **名稱**： 顯示的值**名稱**屬性。 輸入其他名稱即可變更設定。<br /><br /> **使用量**： 指定是否這是 Regular、 Key、 父系或 AccountType 屬性。 按一下此資料行中的值，即可選取其他設定。<br /><br /> **型別**： 指定屬性的商業智慧類別目錄。 按一下此資料格，即可選取其他設定。<br /><br /> **索引鍵資料行**： 顯示 OLE DB 資料類型**KeyColumn**屬性上的屬性。 無法變更此資料行。<br /><br /> **名稱資料行**： 指出是否**NameColumn**屬性上的屬性設定為相同的資料行，做為設定**KeyColumn**屬性。 無法變更此資料行。|  
  
 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，下表裡顯示的圖示會根據屬性的使用方式標示屬性。  
  
|圖示|屬性使用方式|  
|----------|---------------------|  
|![屬性圖示](../media/as-icon-attribute.gif "屬性圖示")|Regular 或 AccountType|  
|![索引鍵屬性圖示](../media/as-icon-key-attribute.gif "索引鍵屬性圖示")|索引鍵|  
|![父屬性圖示](../media/as-icon-parent-attribute.gif "父屬性圖示")|父系|  
  
## <a name="see-also"></a>另請參閱  
 [維度屬性內容參考](dimension-attribute-properties-reference.md)  
  
  
