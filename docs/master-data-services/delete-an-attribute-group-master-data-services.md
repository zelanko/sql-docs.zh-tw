---
description: 刪除屬性群組 (Master Data Services)
title: 刪除屬性群組
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting attribute groups [Master Data Services]
- attribute groups [Master Data Services], deleting
ms.assetid: f915e89b-629d-4725-aea6-a7f051978244
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 91abdbbec357c5d5b7b629c5619b221c14bc0d15
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500582"
---
# <a name="delete-an-attribute-group-master-data-services"></a>刪除屬性群組 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，如果 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的 [總管]**** 功能區域已不再需要顯示某個索引標籤時，您即可刪除該屬性群組。  
  
-   **注意**：當屬性群組存在時，[總管]**** 只會顯示屬於該屬性群組的屬性。 當屬性群組不存在時，則會顯示所有屬性。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-delete-an-attribute-group"></a>若要刪除屬性群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [ **管理模型** ] 頁面上，從方格中選取模型，然後按一下 [ **實體**]。  
  
3.  在 [管理實體]**** 頁面上，從方格中選取含有您想要編輯其屬性群組之實體的資料列。  
  
4.  按一下 [屬性群組]****。  
  
5.  在 [管理屬性群組]**** 頁面上，依據您想要刪除的群組類型，從 [成員類型]**** 下拉式清單中選取成員類型，再展開 [分葉]****、[合併]**** 或 [集合]****。  
  
6.  按一下您要刪除的屬性群組。  
  
7.  按一下 **[刪除]** 。  
  
8.  在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [屬性群組 &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [建立屬性群組 &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
