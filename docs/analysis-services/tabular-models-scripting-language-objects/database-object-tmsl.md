---
title: "資料庫物件 (TMSL) |Microsoft 文件"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ae5c046b-8242-4046-ae76-2c070503fd93
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d10567517408ad6789b5b4aad9dbb7dcd3f92d2b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="database-object-tmsl"></a>資料庫物件 (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  定義表格式資料庫相容性層級 1200年或更高，相同層級的模型為基礎。 本主題將說明物件定義的資料庫，提供裝載之要求的建立、 修改、 刪除和執行資料庫管理工作。  
  
> [!NOTE]  
>  任何指令碼，只有一個資料庫時，可參考。 資料庫本身以外的任何物件，資料庫屬性是選擇性，如果您指定的模型。 沒有模型，可用來推算的資料庫名稱，如果未明確提供的資料庫之間具有一對一對應。   
> 同樣地，您可以不處理模型，在資料庫上設定其屬性。  
  
## <a name="object-definition"></a>物件定義  
 所有物件都具有一組常用的屬性，包括名稱、 類型、 描述、 屬性集合，以及註解。 **資料庫**物件也有下列屬性。  
  
 compatibilitylevel  
 目前，有效值為 1200，1400年。 較低的相容性層級使用不同的中繼資料引擎。  
  
 readwritemode  
 列舉資料庫的模式。 通常會讓在高可用性或延展性設定唯讀的資料庫。 有效值包括 readWrite，  
                readOnly，  
                或 readOnlyExclusive。 請參閱[Analysis Services 的高可用性與延展性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)和[切換 ReadOnly 和 ReadWrite 模式之間的 Analysis Services 資料庫](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)如需有關使用這個屬性時。  
  
## <a name="usage"></a>使用方式  
 **資料庫**幾乎每個命令會使用物件。 請參閱[命令中表格式模型指令碼語言 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)清單。 A**資料庫**物件是伺服器物件的子系。  
  
 建立時，取代或改變資料庫物件，指定物件定義的所有讀寫屬性。 省略的讀 / 寫屬性會被視為刪除。  
  
## <a name="partial-syntax"></a>部分語法  
 因為這個物件定義是很大，則會列出只有直接屬性。 **模型**物件提供大量的資料庫定義。 請參閱[模型物件 &#40;TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)來定義物件的方式。  
  
```  
    "database": {  
      "type": "object",  
      "properties": {  
        "name": {  
          "type": "string"  
        },  
        "id": {  
          "type": "string"  
        },  
        "description": {  
          "type": "string"  
        },  
        "compatibilityLevel": {  
          "type": "integer"  
        },  
        "readWriteMode": {  
          "enum": [  
            "readWrite",  
            "readOnly",  
            "readOnlyExclusive"  
          ]  
        },  
        "model": {  
          "type": "object",  
          ...  
        }  
    }  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 的高可用性與延展性](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)  
  
  

