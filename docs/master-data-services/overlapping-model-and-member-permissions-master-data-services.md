---
title: "重疊的模型和成員的權限 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "模型 [Master Data Services], 有效權限"
  - "權限 [Master Data Services], 模型和成員重疊"
  - "成員 [Master Data Services], 有效權限"
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 重疊的模型和成員的權限 (Master Data Services)
  指派給成員的權限可能會與指派給模型物件的權限重疊。 當發生重疊情況時，比較嚴格的權限會生效。  
  
 如果成員擁有的權限與其對應模型物件的權限不同，則會套用下列規則：  
  
-   **拒絕** 覆寫所有其他權限。  
  
-   **系統管理員** 權限模型層級會覆寫所有其他權限，以及變更為 sub 層級上的所有 (CRUD) 存取權限。  
  
-   有效存取權限會與成員和屬性的權限交集。  
  
     例如，如果成員權限包括 **建立** 和 **更新**, ，屬性的權限是 **更新**。 有效權限是 **更新**。  
  
 下圖顯示當屬性權限與成員權限不同時，個別屬性值的哪些權限會生效。  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## 範例 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 在 **模型** 索引標籤上，Product 實體有 **更新** 指派權限。 此實體中的所有屬性都會繼承該權限。  
  
 在 **階層成員** 索引標籤上，衍生階層中的 Mountain Bikes 子類別目錄節點已 **更新** 指派權限。  
  
 結果︰ 在 **總管**, ，使用者擁有 **更新** Mountain Bikes 節點中的所有成員的所有屬性值的權限。 系統會隱藏所有其他成員和屬性。  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## 範例 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 在 **模型** 索引標籤上，Subcategory 屬性已 **更新** 指派權限。  
  
 在 **階層成員** 索引標籤上，明確指派衍生階層中的 Mountain Bikes 子類別目錄節點 **讀取** 權限。  
  
 結果︰ 在 **總管**, ，使用者可以 **讀取** Subcategory 屬性值 [越野車] 節點中之成員的權限。 系統會隱藏所有其他成員和屬性。  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## 範例 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 在 **模型** 索引標籤上，Subcategory 屬性已 **讀取** 指派權限。  
  
 在 **階層成員** 索引標籤上，明確指派衍生階層中的 Mountain Bikes 子類別 **更新** 權限。  
  
 結果︰ 在 **總管**, ，使用者擁有 **讀取** 屬性值的權限。 系統會隱藏所有其他成員和屬性。  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## 另請參閱  
 [如何決定權限 & #40。Master Data Services & #41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [重疊的使用者和群組的權限 & #40。Master Data Services & #41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  