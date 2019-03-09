---
title: Analysis Services 表格式模型物件層級安全性 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d354aa64e8b6a1e98941011c30550a056f4c01c9
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685574"
---
# <a name="object-level-security"></a>物件層級安全性
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
資料模型的安全性是以有效地實作[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)和資料列層級篩選，來定義資料模型物件和資料的使用者權限。 從表格式 1400年模型，您也可以定義物件層級安全性，包括資料表層級的安全性和中的資料行層級安全性[Roles 物件](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)。

## <a name="table-level-security"></a>資料表層級的安全性

使用資料表層級的安全性，您可以不只限制存取資料表資料，但也敏感的資料表名稱，協助防止惡意使用者探索，如果資料表存在。 

 資料表層級的安全性設定中 Model.bim，JSON 為基礎的中繼資料內[表格式模型指令碼語言 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)，或[表格式物件模型 (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)。 設定**metadataPermission**屬性**tablePermissions**類別[角色物件](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)至**無**。

在此範例中，Product 資料表的 tablePermissions 類別的 metadataPermission 屬性設為 無：

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

類似於資料表層級的安全性，資料行層級安全性與您可以不只限制存取的資料行資料，但機密的資料行名稱，協助防止惡意使用者探索的資料行。

 在 Model.bim，JSON 為基礎的中繼資料中設定資料行層級安全性[表格式模型指令碼語言 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)，或[表格式物件模型 (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)。 設定**metadataPermission**屬性**columnPermissions**類別[角色物件](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)至**無**。

在此範例中，[員工] 資料表中的基底費率] 資料行的 columnPermissions 類別的 metadataPermission 屬性設為 [無：

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

*  如果中斷關聯性鏈結，無法設定資料表層級的安全性模型。 在設計階段，會產生錯誤。
 例如，如果有資料表 A 和 B，B 和 C 之間的關聯性，您無法保護資料表 b。如果保護資料表 B，資料表 A 上的查詢無法轉換資料表 A 和 B，B 和 c 之間的關聯性在此情況下，可以設定個別的關聯性之間資料表 A 和 b。

    ![資料表層級的安全性](../../analysis-services/tabular-models/media/ssas-ols.png)  


*  因為它引入非預期的存取受保護的資料，無法從不同的角色合併資料列層級安全性和物件層級安全性。 在這種組合，角色的成員使用者的查詢時，會產生錯誤。

*  動態計算 （量值、 Kpi、 DetailRows） 會自動限制，前提是它們參考的受保護的資料表或資料行。 雖然沒有任何機制來明確地保護 量值，就能夠以隱含方式來保護量值更新到安全的資料表或資料行參考運算式。

*  參考的受保護的資料行的關聯性工作提供的資料行的資料表並未受到保護。




## <a name="see-also"></a>另請參閱  
[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
[Roles 物件 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/roles-object-tmsl)  
[表格式模型指令碼語言 (TMSL)](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)  
[表格式物件模型 (TOM)](https://docs.microsoft.com/bi-reference/tom/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo)。

  
