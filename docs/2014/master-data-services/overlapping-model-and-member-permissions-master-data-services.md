---
title: 重疊的模型和成員的權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], effective permissions
- permissions [Master Data Services], model and member overlaps
- members [Master Data Services], effective permissions
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9129b2290480287be6188e8bf7b2c3181b42cea1
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960802"
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>重疊的模型和成員的權限 (Master Data Services)
  指派給成員的權限可能會與指派給模型物件的權限重疊。 當發生重疊情況時，比較嚴格的權限會生效。  
  
 如果成員擁有的權限與其對應模型物件的權限不同，則會套用下列規則：  
  
-   **[拒絕]** 會覆寫所有其他的權限。  
  
-   **唯讀**覆寫**更新**。  
  
 下圖顯示當屬性權限與成員權限不同時，個別屬性值的哪些權限會生效。  
  
 ![mds_conc_security_member_overlap_table](../../2014/master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## <a name="example-1"></a>範例 1  
 ![mds_conc_overlap_model_1](../../2014/master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 在 **[模型]** 索引標籤上，Product 實體已被指派 **[更新]** 權限。 此實體中的所有屬性都會繼承該權限。  
  
 在 **[階層成員]** 索引標籤上，衍生階層中的 Mountain Bikes 子類別目錄節點已被指派 **[更新]** 權限。  
  
 結果：在 **[總管]** 中，使用者擁有 Mountain Bikes 節點中所有成員之所有屬性值的 **[更新]** 權限。 系統會隱藏所有其他成員和屬性。  
  
 ![mds_conc_overlap_model_example_1](../../2014/master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## <a name="example-2"></a>範例 2  
 ![mds_conc_overlap_model_2](../../2014/master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 在 **[模型]** 索引標籤上，Subcategory 屬性已被指派 **[更新]** 權限。  
  
 在 [階層**成員**] 索引標籤上，衍生階層中的 [山區自行車子類別目錄] 節點會明確指派 [**唯讀**] 許可權。  
  
 結果：在**Explorer**中，使用者對 [山區自行車] 節點中成員的子類別屬性值具有 [**唯讀**] 許可權。 系統會隱藏所有其他成員和屬性。  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="example-3"></a>範例 3  
 ![mds_conc_overlap_model_3](../../2014/master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 在 [**模型**] 索引標籤上，[子類別目錄] 屬性已獲指派 [**唯讀**] 許可權。  
  
 在 **[階層成員]** 索引標籤上，衍生階層中的 Mountain Bikes 子類別目錄已被明確指派 **[更新]** 權限。  
  
 結果：在 [ **Explorer**] 中，使用者擁有屬性值的 [**唯讀**] 許可權。 系統會隱藏所有其他成員和屬性。  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="see-also"></a>另請參閱  
 [如何判斷許可權 &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)   
 [重疊的使用者和群組的權限 &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  
