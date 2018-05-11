---
title: 表格式模型物件層級安全性 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8b8aab3830971bfeb0438a1f890c11889374c803
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="object-level-security"></a>物件層級安全性
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
資料模型的安全性是以有效地實作[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)和資料列層級篩選，來定義使用者權限的資料模型物件和資料。 從開始 1400年的表格式模型，您也可以定義物件層級安全性，包括資料表層級的安全性和中的資料行層級安全性[角色物件](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)。

## <a name="table-level-security"></a>資料表層級的安全性

使用資料表層級的安全性，您可以不只限制存取資料表資料，但也機密的資料表名稱，協助防止惡意使用者探索，如果資料表存在。 

 資料表層級的安全性設定 JSON 型中繼資料內 Model.bim [Tabular Model Scripting Language (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)，或[表格式物件模型 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)。 設定**metadataPermission**屬性**tablePermissions**類別[角色物件](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)至**無**。

在此範例中，metadataPermission tablePermissions 類別針對 Product 資料表是設定為 none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Product",
        "metadataPermission": "none"
      }
    ]
  }
```

## <a name="column-level-security"></a>資料行層級安全性

類似於使用資料行層級安全性的資料表層級安全性，您可以不只限制存取資料行資料，但機密的資料行名稱，協助防止惡意使用者探索的資料行。

 資料行層級安全性設定 JSON 型中繼資料內 Model.bim [Tabular Model Scripting Language (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)，或[表格式物件模型 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)。 設定**metadataPermission**屬性**columnPermissions**類別[角色物件](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)至**無**。

在此範例中，metadataPermission 屬性 columnPermissions 為之類別的基底速率中的資料行 [員工] 資料表設定為 none:

```
"roles": [
  {
    "name": "Users",
    "description": "All allowed users to query the model",
    "modelPermission": "read",
    "tablePermissions": [
      {
        "name": "Employee",
        "columnPermissions": [
          {
            "name": "Base Rate",
            "metadataPermission": "none"
          }
        ]
      }
    ]
  }
```

## <a name="restrictions"></a>限制

*  如果中斷了關聯性鏈結，無法設定資料表層級的安全性模型。 在設計階段，會產生錯誤。
 例如，如果資料表 A 和 B，B 和 C 之間的關聯性，您不能保護資料表 b。如果受保護資料表 B，資料表 A 上的查詢無法傳輸資料表 A 和 B，B 和 c 之間的關聯性在此情況下，無法在資料表 A 和 b 之間設定個別的關聯性

    ![資料表層級的安全性](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  資料列層級安全性和物件層級安全性無法結合來自不同的角色，因為它引入非預期的存取受保護的資料。 在查詢時，如果使用者是這類的組合角色的成員會產生錯誤。

*  動態計算 （量值、 Kpi、 DetailRows） 會自動限制，前提是它們參考的安全的資料表或資料行。 沒有機制來明確安全量值時，它就能夠以隱含方式來保護量值更新到安全的資料表或資料行參考運算式。

*  參考的受保護的資料行的關聯性工作提供的資料行的資料表並不安全。




## <a name="see-also"></a>另請參閱  
[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Roles 物件 (TMSL)](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)  
[表格式模型指令碼語言 (TMSL)](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
[表格式物件模型 (TOM)](../../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md)。

  
