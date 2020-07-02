---
title: 讓使用者看到屬性群組
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 998eed940f93c90974848812e0e6dabf7cf9ca91
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811736"
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>讓使用者看到屬性群組 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  當您希望使用者在總管**** 功能區域的方格上方有索引標籤時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中對使用者或群組顯示屬性群組。  
  
 當您建立屬性群組時，它會自動隱藏起來不讓所有使用者看到，除了建立它的使用者以外。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
-   至少有一個屬性群組必須存在。 如需詳細資訊，請參閱 [建立屬性群組 &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)(管理員 (Master Data Services))。  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>若要讓使用者看到屬性群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [**管理模型**] 頁面上，從方格中選取模型，然後按一下 [**實體**]。  
  
3.  在 [管理實體]**** 頁面上，從方格中選取含有您想要編輯屬性群組之實體的資料列。  
  
4.  按一下 [屬性群組]****。  
  
5.  在 [管理屬性群組]**** 頁面上，取決於您想要顯示的群組類型，從 [成員類型]**** 下拉式清單方塊中選取成員類型，展開 [分葉]****、[合併]**** 或 [集合]****。  
  
6.  選取您想要從方格中編輯的屬性群組，然後按一下 [編輯]****。  
  
7.  按一下 [可用]**** 方塊中的使用者或群組，然後按一下 [加入]**** 箭號。 若要全部加入，請按一下 [全部加入]**** 箭號。  
  
8.  按一下 [檔案] 。  
  
## <a name="see-also"></a>另請參閱  
 [屬性群組 &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [建立屬性群組 &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
