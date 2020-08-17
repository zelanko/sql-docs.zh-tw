---
description: 排除商務規則 (Master Data Services)
title: 排除商務規則
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bc69a5cfcd36e96ed6bc0778c72e6a3a09e6fb23
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88388954"
---
# <a name="exclude-a-business-rule-master-data-services"></a>排除商務規則 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您不想要永久刪除商務規則，但是也不想使用它來驗證資料時，可排除此商務規則。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-exclude-a-business-rule"></a>若要排除商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [ **商務規則** ] 頁面上，從 [ **模型** ] 下拉式清單中選取模型。  
  
4.  從 [實體] **** 下拉式清單選取實體。  
  
5.  從 [成員類型]**** 下拉式清單中，選取成員的類型。  
  
6.  在方格中，選取您想要排除之商務規則的資料列，然後按一下 [編輯]****。  
  
7.  選取 [已排除]**** 核取方塊。  
  
8.  按一下 [檔案] 。  
  
9. 按一下 [全部發行] ****。  
  
10. 在確認對話方塊中按一下 **[確定]**。 [商務規則狀態]**** 資料行中的值是 [已排除]**** 且 [已排除]**** 資料行是 [是]****。  
  
## <a name="see-also"></a>另請參閱  
 [刪除商務規則 &#40;Master Data Services&#41;](../master-data-services/delete-a-business-rule-master-data-services.md)   
 [建立和發佈商務規則 &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
