---
title: "可寫入維度 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- write-enabled dimensions [Analysis Services]
- dimensions [Analysis Services], write-enabled
- dimension writeback [Analysis Services]
- write-enabled cubes [Analysis Services]
- writeback [Analysis Services], dimensions
ms.assetid: 0bac050d-cd3b-427b-884a-65a91be89500
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bde831aea891db84e76ae4d00612663ed315d869
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="write-enabled-dimensions"></a>可寫入維度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 維度中的資料通常是唯讀的； 但是在某些狀況下，您可能會希望維度是可寫入的。 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，寫入-維度讓商務使用者可以修改與維度的內容，並查看變更的立即影響維度的階層上。 以單一資料表為根據的任何維度皆可寫入； 在可寫入維度中，商務使用者和管理員可以變更、移動、加入及刪除此維度中的屬性成員。 這些更新統稱為*維度回寫*。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援所有維度屬性上的維度回寫，並修改維度的任何成員。 如果是可寫入的 Cube 或資料分割，會將更新儲存在與 Cube 來源資料表分開的回寫資料表中。 不過，針對可寫入維度，更新會直接記錄在維度的資料表中。 而且，如果可寫入維度是包含在有多個資料分割的 Cube 中，其中部分或全部資料來源具有維度資料表的副本，則在回寫程序中只更新原始維度資料表。  
  
 可寫入維度和可寫入 Cube 的功能不同，但可互補。 可寫入維度讓商務使用者有能力更新成員，而可寫入 Cube 則讓他們有能力更新資料格值。 雖然這兩個功能是互補的，但您並不需要將二者組合使用。 維度不一定要包含在 Cube 中，照樣可發生維度回寫。 可寫入維度也可包括於非可寫入的 Cube 中。 使用不同的程序來讓維度和 Cube 可寫入，並維護它們的安全性。  
  
 下列限制適用於維度回寫：  
  
-   建立新的成員時，您必須包含維度中的每個屬性。 您不能插入成員時不指定維度之索引鍵屬性的值。 因此，建立成員時要受到維度資料表上之已定義的任何條件約束 (例如非 Null 索引鍵值)。  
  
-   只針對星狀結構描述支援維度回寫。 換句話說，維度必須以和事實資料表直接相關的單一維度資料表為基礎。 使維度可寫入之後，當您部署到現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫或建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會驗證此需求。  
  
 您可以修改或刪除回寫維度的任何現有成員。 刪除成員時，刪除動作會串聯到所有子成員。 例如，在包含 CountryRegion、省份、縣 (市) 以及客戶屬性的客戶維度中，刪除某個國家 (地區) 會同時刪除隸屬於該國家 (地區) 的所有省份、縣 (市) 以及客戶。 如果國家 (地區) 只有一個省份，刪除該省份也會同時刪除國家 (地區)。  
  
 回寫維度的成員只能在相同層級內移動。 例如，可以將縣 (市) 移動到不同國家 (地區) 或省份的縣 (市) 層級，但不能將縣 (市) 移動到省份或 CountryRegion 層級。 在父子式階層中，所有成員都是分葉成員，因此成員可能會移至任何層級以外**（全部）**層級。  
  
 如果刪除父子式階層的成員，則成員的子系會移至該成員的父系。 在刪除的成員上必須要有關聯式資料表的更新權限，而在移動的成員上則不需要任何權限。 應用程式在父子式階層中移動成員時，應用程式可以在 UPDATE 作業中指定成員的下階是否跟著成員一起移動，或是移到成員的父系。 若要遞迴地刪除父子式階層中的成員，使用者對於該成員和所有成員的下階必須有關聯式資料表的更新權限。  
  
> [!NOTE]  
>  父子式階層中之父屬性的更新，不可包含任何其他屬性 (Property) 或屬性 (Attribute) 的更新。  
  
 維度的所有變更會造成維度結構遭到修改。 維度的每個變更會被視為單一交易，需要累加處理來更新維度結構。 可寫入維度與其他任何維度具有相同的處理需求。  
  
> [!NOTE]  
>  連結維度不支援維度回寫。  
  
## <a name="security"></a>安全性  
 唯一可以更新可寫入維度的商務使用者，是那些在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫角色中被授權對該維度有讀取/寫入權限的使用者。 針對每個角色，您可以控制哪些成員可以或不可以被更新。 針對要更新可寫入維度的商務使用者，其用戶端應用程式必須支援此能力。 如果是這類使用者，可寫入維度必須包含在該維度上次變更之後處理過的 Cube 中。 如需詳細資訊，請參閱[物件和作業的存取權授權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)。  
  
 管理員角色中所含的使用者和群組可以更新可寫入維度的屬性成員，即使該維度未包括在 Cube 中也一樣。  
  
## <a name="see-also"></a>請參閱  
 [資料庫維度屬性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [可寫入的資料分割](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [維度 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
