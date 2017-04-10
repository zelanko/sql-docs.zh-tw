---
title: "要求屬性值 (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "商務規則 [Master Data Services], 要求屬性值"
  - "屬性 [Master Data Services], 要求值"
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# 要求屬性值 (Master Data Services)
  當您想要確保主要資料完整時，在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中要求屬性值。  
  
> [!NOTE]  
>  在以網域屬性關聯性為基礎的衍生階層中，不會顯示遺漏網域屬性值的成員。  
  
## 必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員及 #40。Master Data Services & #41;](../master-data-services/administrators-master-data-services.md)。  
  
### 若要要求屬性值  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列指向 **管理** 按一下 **商務規則**。  
  
3.  在 **商務規則** ] 頁面上，從 **模型** 下拉式清單中，選取的模型。  
  
4.  從 **實體** 下拉式清單中，選取的實體。  
  
5.  從 **成員型別** 下拉式清單中，選取来套用至商務規則成員的型別。  
  
6.  按一下 **[加入]**。  
  
7.  在 **名稱** 方塊中，輸入商務規則的名稱。  
  
8.  （選擇性） 在 **描述** 欄位中，輸入商務規則的描述。  
  
9. 在 **然後** 區塊中，按一下 [ **新增**。 面板隨即出現。  
  
10. 從 **運算子** 下拉式清單中，選取 **所需動作**。  
  
11. 從 **屬性** 下拉式清單中，選取一個屬性。  
  
12. 按一下 **[儲存]**。 新的資料列會加入至 **然後** 方格。  
  
13. 按一下 **[儲存]**。  
  
14. 按一下 [ **發行所有**。  
  
15. 在確認對話方塊中按一下 **[確定]**。 中的值 **商務規則的狀態** 資料行是 **Active**。  
  
## 後續步驟  
  
-   遵循下列其中一個程序，將商務規則套用至資料：  
  
    -   [根據商務規則和 #40; 驗證特定成員Master Data Services & #41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [根據商務規則和 #40; 驗證版本Master Data Services & #41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## 另請參閱  
 [商務規則和 #40。Master Data Services & #41;](../master-data-services/business-rules-master-data-services.md)   
 [衍生的階層 & #40。Master Data Services & #41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  