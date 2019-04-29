---
title: 刪除商務規則 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 652b301a91adc3c6c417e23ff2f192712c5f4a04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62924961"
---
# <a name="delete-a-business-rule-master-data-services"></a>刪除商務規則 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，刪除不再需要的商務規則。  
  
> [!NOTE]  
>  您可以避免資料使用商務規則來加以驗證，其方式是排除該商務規則，而不是將它刪除。 如需詳細資訊，請參閱[排除商務規則 &#40;Master Data Services&#41;](exclude-a-business-rule-master-data-services.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-delete-a-business-rule"></a>若要刪除商務規則  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  從功能表列，指向 **[管理]** ，然後按一下 **[商務規則]**。  
  
3.  在 [商務規則維護] 頁面上，選取 [模型] 清單中的模型。  
  
4.  從 [實體] 清單中選取實體。  
  
5.  從 [成員類型] 清單中，選取要套用商務規則的成員類型。  
  
6.  從 [屬性] 清單中，選取屬性或保留預設值 [全部]。  
  
7.  在方格中，按一下您想要刪除之商務規則的資料列。  
  
8.  按一下 **刪除選取的商務規則**。  
  
9. 在確認對話方塊中按一下 **[確定]**。 中的值**狀態**資料行是**刪除暫止**。  
  
10. 按一下 [發行商務規則]。  
  
11. 在確認對話方塊中按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [排除商務規則 &#40;Master Data Services&#41;](exclude-a-business-rule-master-data-services.md)   
 [建立及發行商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
