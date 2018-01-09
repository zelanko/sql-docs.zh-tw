---
title: "模型物件 (TMSL) |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 9382d0d6-2d4b-49ad-a0eb-35970f0f3afb
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dadb4807613b23449fd87dfea35acc0d6d201615
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="model-object-tmsl"></a>模型物件 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]定義表格式模型。 沒有一個模型，每個資料庫和只有一個可以在任何指定的命令中指定的資料庫。 資料庫物件是父系物件。  
  
 模型定義太大而無法重現整個語法中的主題。 基於這個理由，反白顯示的主要組件部分語法可以找到下，子物件的連結。  
  
 可能是了解模型定義的最佳方式是從您很了解表格式模型開始。 使用**檢視程式碼**SQL Server Data Tools 中檢視其定義的選項。 請記住安裝 JSON 編輯器，讓您可以檢視程式碼。 您可以在 Visual Studio 中取得 JSON 編輯器[下載 Community edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)或其他版本的 Visual Studio。  
  
> [!NOTE]  
>  任何指令碼，只有一個資料庫時，可參考。 資料庫本身以外的任何物件，資料庫屬性是選擇性，如果您指定的模型。 沒有模型，可用來推算的資料庫名稱，如果未明確提供的資料庫之間具有一對一對應。   
> 同樣地，您可以不處理模型，在資料庫上設定其屬性。  
  
## <a name="object-definition"></a>物件定義  
 所有物件都具有一組常用的屬性，包括名稱、 類型、 描述、 屬性集合，以及註解。 **模型**物件也有下列屬性。  
  
 storageLocation  
 磁碟上放置模型的位置。  
  
 defaultMode  
 讓資料可在分割區中使用的預設方法。  
  
 defaultDataView  
 針對在 DirectQuery 模式的模型，這個屬性會決定哪些資料分割會用來對模型執行查詢。  有效值包括完整和範例。  
  
 culture (文化特性)  
 要用來格式化的文化特性。  
  
 collation  
 定序序列。 請參閱[Analysis Services 的全球化案例](../../analysis-services/globalization-scenarios-for-analysis-services.md)如需詳細資訊。  
  
 資料表  
 完整資料表在模型中，包括資料分割、 資料行、 量值、 Kpi 和註解的集合。 請參閱[資料表物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)如需詳細資訊。  
  
 關聯性  
 指定每一對資料表，其中包含設定篩選方向和安全性的屬性之間的關聯性。 請參閱[關聯性物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)如需詳細資訊。  
  
 資料來源  
 一或多個連接至外部資料庫提供資料給模型，或使用通過查詢。 請參閱[資料來源物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)如需詳細資訊。  
  
 角色  
 將資料庫權限、 成員的帳戶，和 （選擇性） 在 DAX 中的自訂存取控制的安全性篩選相關聯的物件。  
  
## <a name="usage"></a>使用方式  
 **模型**物件包含整個模型。 您必須指定一個模型和/或其父資料庫物件中的大部分命令。  
  
 建立時，取代或改變模型的物件，指定物件定義的所有讀寫屬性。 省略的讀 / 寫屬性會被視為刪除。  
  
## <a name="partial-syntax"></a>部分語法  
 因為這個物件定義是很大，則會列出只有第一個層級的屬性。 請參閱[物件定義的表格式模型指令碼語言 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)子物件的清單。  
  
```  
    "model": {  
      "description": "Model object of a Tabular database",  
      "type": "object",  
      "properties": {  
          "name": {  },  
          "description": {  },  
         "storageLocation": {  },  
         "defaultMode":  {  },  
         "defaultDataView": {  },  
         "culture": {  },  
         "collation": {  },  
         "annotations": {  },  
         "tables": {  },  
         "relationships": {  },  
         "dataSources": {  },  
         "perspectives": {  },  
            "cultures": {  },  
         "roles": {  }  
    }  
  
```  
  
## <a name="see-also"></a>請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
