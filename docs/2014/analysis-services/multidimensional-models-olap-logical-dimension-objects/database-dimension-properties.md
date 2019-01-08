---
title: 資料庫維度屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- metadata [Analysis Services]
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 075548ef-08a3-413c-8ee0-4a074c276fcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 34de23fca71f4dc7949a04a36323d19d35826fa9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359820"
---
# <a name="database-dimension-properties"></a>資料庫維度屬性
  在  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，維度的特性由維度，根據各種維度屬性的設定和屬性或階層維度所包含的中繼資料定義。 下表描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的維度屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|`AttributeAllMemberName`|針對維度中的屬性，指定所有成員的名稱。|  
|`Collation`|決定維度使用的定序。|  
|`CurrentStorageMode`|包含維度的目前儲存模式。|  
|`DependsOnDimension`|包含維度所相依之其他維度的識別碼，如果有的話。|  
|`Description`|包含維度的描述。|  
|`ErrorConfiguration`|用來處理重複的索引鍵、未知的索引鍵、錯誤限制、發生錯誤時的動作、錯誤記錄檔，以及 Null 索引鍵處理之可設定的錯誤處理設定。|  
|`ID`|包含維度的唯一識別碼 (ID)。|  
|`Language`|指定維度的預設語言。|  
|`MdxMissingMemberMode`|決定如何處理多維度運算式 (MDX) 陳述式的遺漏成員。|  
|`MiningModelID`|包含與資料採礦維度相關之採礦模型的識別碼。 只有在維度是採礦模型維度時，才可使用這個屬性。|  
|`Name`|指定維度的名稱。|  
|`ProactiveCaching`|定義維度的主動式快取設定。|  
|`ProcessingGroup`|指定處理群組。 值為 ByAttribute 或 ByTable。 預設值是 `ByAttribute`。|  
|`ProcessingMode`|指出是否應在處理期間或處理之後，進行索引和彙總 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。|  
|`ProcessingPriority`|決定背景作業期間之維度的處理優先權 (例如，延遲彙總、索引或叢集)。|  
|`Source`|識別維度所繫結的資料來源檢視。|  
|`StorageMode`|決定維度的儲存模式。|  
|`Type`|指定維度的類型。|  
|`UnknownMember`|指出未知的成員是否可見。|  
|`UnknownMemberName`|指定維度之未知成員的標題，而這個標題會以維度的預設語言顯示。|  
|`WriteEnabled`|指出是否可以使用維度回寫 (受限於安全性權限)。|  
  
> [!NOTE]  
>  如需有關如何設定 ErrorConfiguration 和 UnknownMember 屬性值，當使用 null 值和其他資料完整性議題的詳細資訊，請[Analysis Services 2005 中處理資料完整性問題](https://go.microsoft.com/fwlink/?LinkId=81891)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](attributes-and-attribute-hierarchies.md)   
 [使用者階層](user-hierarchies.md)   
 [維度關聯性](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [維度 &#40;Analysis Services-多維度資料 &#41;](dimensions-analysis-services-multidimensional-data.md)  
  
  
