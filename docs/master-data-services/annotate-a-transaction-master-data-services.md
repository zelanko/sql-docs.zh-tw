---
title: "為交易加上註解 (Master Data Services) | Microsoft Docs"
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
  - "註解 [Master Data Services], 針對交易"
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# 為交易加上註解 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，當您想要提供有關某個交易的支援詳細資料做為歷程記錄時，請為該交易加上註解。  
  
> [!NOTE]  
>  您無法刪除註解。  
  
## 必要條件  
  
-   若要為所建立的交易加上註解，您必須擁有存取 [總管] 功能區域的權限，而且至少必須擁有您要加上註解之模型物件的**更新**權限。  
  
-   若要為所有使用者的交易加上註解，您必須擁有存取 [版本管理] 功能區域的權限，而且必須身為模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### 若要在總管中為交易加上註解  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，選取 [模型]  清單中的模型。  
  
2.  從 **[版本]** 清單中選取版本。  
  
3.  按一下 **[總管]**。  
  
4.  從功能表列指向 [實體]，然後按一下包含成員且具有您要加上註解之交易的實體。  
  
5.  在方格中，按一下成員的資料列。  
  
6.  按一下 [檢視交易]。  
  
7.  在 [檢視交易] 對話方塊中，按一下您要加上註解的交易。  
  
8.  在對話方塊底部的方塊中，輸入您的註解。  
  
9. 按一下 [加入註解]。 註解就會顯示在 [註解] 窗格中。  
  
### 若要在版本管理中為交易加上註解 (僅限系統管理員)  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，按一下 [版本管理]。  
  
2.  在功能表列上，按一下 [交易]。  
  
3.  在 [交易] 窗格中，針對您想要加上註解的交易，按一下方格中的資料列。  
  
4.  在 [交易註解] 窗格的 [註解] 方塊中，輸入您的註解。  
  
5.  按一下 **[確定]**。  
  
## 另請參閱  
 [註解 &#40;Master Data Services&#41;](../master-data-services/annotations-master-data-services.md)   
 [交易 &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  