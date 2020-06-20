---
title: 自動產生 Code 屬性值 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4de63eefe9bdd1f6957a59917bf1a8aec6d74f0d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972158"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>自動產生 Code 屬性值 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中，當您希望每次建立新成員時，自動將整數指派給 Code 值，請自動為實體的 Code 屬性產生值。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)。  
  
-   實體必須存在。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-automatically-generate-code-values"></a>若要自動產生值字碼  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [**模型瀏覽器**] 頁面上，從功能表列指向 [**管理**]，然後按一下 [**實體**]。  
  
3.  在 **[實體維護]** 頁面上，選取 **[模型]** 清單中的模型。  
  
4.  選取要產生其字碼之實體的資料列。  
  
5.  按一下 **[編輯選取的實體]**。  
  
6.  選取 **[自動建立字碼值]** 核取方塊。  
  
7.  在 **[開始]** 方塊中，輸入開始遞增的數字。 如果成員已存在，則將根據最大的現有值設定 Code。 例如，若最大的現有 Code 值為 299，則下一個成員的 Code 值將設為 300。  
  
8.  按一下 [**儲存實體**]。  
  
## <a name="see-also"></a>另請參閱  
 [自動建立程式碼 &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)   
 [自動產生 Code 以外的屬性值 &#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
