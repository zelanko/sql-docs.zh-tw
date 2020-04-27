---
title: 排除商務規則 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], excluding
ms.assetid: bdbc9df0-23f7-40b9-8aba-4445c1482580
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8f18e047b11bee4093ce7a6e494c1ae1bf3d0ada
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65483379"
---
# <a name="exclude-a-business-rule-master-data-services"></a>排除商務規則 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您不想要永久刪除商務規則，但是也不想使用它來驗證資料時，可排除此商務規則。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
### <a name="to-exclude-a-business-rule"></a>若要排除商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護]**** 頁面上，選取 [模型]**** 清單中的模型。  
  
4.  從 [實體]**** 清單中選取實體。  
  
5.  從 [**成員類型**] 清單中，選取成員的類型。  
  
6.  從 [屬性]**** 清單中，選取屬性或保留預設值 [全部]****。  
  
7.  在方格中，于商務規則的資料列中，選取 [**排除**] 資料行中的核取方塊。 [**狀態**] 資料行中的值為 [**排除暫**止]。  
  
8.  按一下 [發行商務規則]****。  
  
9. 在確認對話方塊中按一下 **[確定]**。 [**狀態**] 資料行中的值已**排除**。  
  
## <a name="see-also"></a>另請參閱  
 [刪除商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)   
 [建立和發佈商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
