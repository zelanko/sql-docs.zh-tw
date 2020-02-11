---
title: ASSL 物件和物件特性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- reference exceptions [Analysis Services Scripting Language]
- ASSL, objects
- inheritance [Analysis Services Scripting Language]
- localized names [Analysis Services Scripting Language]
- objects [Analysis Services Scripting Language]
- names [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
- expansion [Analysis Services Scripting Language]
ms.assetid: 6e5c28b5-c0bc-4ccd-82e5-e174bbb71386
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aee5e7b94aaaca2b35e34f8c4d49c2834189f114
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736612"
---
# <a name="assl-objects-and-object-characteristics"></a>ASSL 物件和物件特性
  Analysis Services 指令碼語言 (ASSL) 中的物件會遵循有關物件群組、繼承、命名、擴展和處理的特定指導方針。  
  
## <a name="object-groups"></a>物件群組  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]所有[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]物件都有 XML 表示。 這些物件分為兩個群組：  
  
 **主要物件**  
 主要物件可以獨立建立、改變和刪除。 主要物件包括：  
  
-   伺服器  
  
-   資料庫  
  
-   維度  
  
-   Cube  
  
-   量值群組  
  
-   資料分割  
  
-   檢視方塊  
  
-   採礦模型  
  
-   角色  
  
-   與伺服器或資料庫相關聯的命令  
  
-   資料來源  
  
 主要物件具有下列可追蹤其記錄與狀態的屬性。  
  
-   `CreatedTimestamp`  
  
-   `LastSchemaUpdate`  
  
-   
  `LastProcessed` (在適當處)  
  
> [!NOTE]  
>  將物件分類為主要物件會影響 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體處理 (Treat)該物件的方式，以及如何以物件定義語言處理 (Handle) 該物件。 不過，這個分類無法保證 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理與開發工具，將允許獨立地建立、修改或刪除這些物件。  
  
 **次要物件**  
 次要物件只能在父主要物件的建立、修改或刪除過程中，建立、修改或刪除。 次要物件包括：  
  
-   階層和層級  
  
-   屬性  
  
-   量值  
  
-   採礦模型資料行  
  
-   與 Cube 相關聯的命令  
  
-   彙總  
  
## <a name="object-expansion"></a>物件展開  
 `ObjectExpansion`限制可用於控制伺服器傳回之 ASSL XML 的擴充程度。 這個限制具有下表中所列的選項。  
  
|列舉值|允許\<Alter>|描述|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|否|只會為要求的物件以及為所有包含的主要物件，遞迴地傳回名稱、識別碼和時間戳記。|  
|*ObjectProperties*|是|展開要求的物件與所含的次要物件，但是不會傳回所含的主要物件。|  
|*ExpandObject*|否|與*ObjectProperties*相同，但也會傳回包含之主要物件的名稱、識別碼和時間戳記。|  
|*ExpandFull*|是|以遞迴方式完全展開要求的物件以及所有包含的物件。|  
  
 這個 ASSL 參考章節描述*ExpandFull*標記法。 所有其他 `ObjectExpansion` 層級都衍生自這個層級。  
  
## <a name="object-processing"></a>物件處理  
 ASSL 包括的唯讀元素或是屬性 (例如 `LastProcessed`)，可以從 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體讀取，但是當將命令指令碼提交到執行個體時，會省略它們。 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會在沒有警告或錯誤的情況下，忽略唯讀元素已修改的值。  
  
 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 也會忽略不適當或是不相關的屬性，而不會引發驗證錯誤。 例如，X 元素應該只有在 Y 元素具有特定值時才出現。 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體會忽略 X 元素，而不會針對 Y 元素值來驗證該元素。  
  
  
