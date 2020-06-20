---
title: 根據商務規則驗證版本 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- validating versions [Master Data Services]
- validating versions [Master Data Services], about validating versions
- versions [Master Data Services], validating
- business rules [Master Data Services], applying to all members
ms.assetid: 5aee7901-6d05-41d4-8bbb-c6f26791d1df
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b6947a01553ebc9bc99e1fef86cf1a6e46c13289
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970962"
---
# <a name="validate-a-version-against-business-rules-master-data-services"></a>根據商務規則驗證版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，驗證版本，以便將商務規則套用到模型版本中的所有成員。  
  
 此程序說明如何使用 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式來驗證資料。 如果您具有 MDS 資料庫的權限，則可以改用預存程序。 如需詳細資訊，請參閱 [驗證預存程序 &#40;Master Data Services&#41;](validation-stored-procedure-master-data-services.md)。  
  
> [!NOTE]  
>  所有成員都必須通過驗證之後，才能認可版本。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[版本管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)。  
  
-   版本的狀態必須是 [開啟]**** 或 [已鎖定]****。  
  
-   在 [驗證版本]**** 頁面上，成員必須存在，且其狀態不得為 [驗證成功]****。  
  
### <a name="to-validate-a-version"></a>若要驗證版本  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]**。  
  
2.  在 [管理版本]**** 頁面上，按一下功能表列上的 [驗證版本]****。  
  
3.  在 [驗證版本]**** 頁面上，選取要驗證的模型和版本。  
  
4.  按一下 **[驗證]** 。  
  
5.  在確認對話方塊中按一下 **[確定]**。  
  
    > [!NOTE]  
    >  不再顯示進度指標時，表示版本已完成驗證。  
  
## <a name="next-steps"></a>後續步驟  
  
-   [鎖定版本 &#40;Master Data Services&#41;](../../2014/master-data-services/lock-a-version-master-data-services.md)  
  
## <a name="see-also"></a>另請參閱  
 [驗證狀態 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-statuses-master-data-services.md)   
 [驗證預存程式 &#40;Master Data Services&#41;](validation-stored-procedure-master-data-services.md)   
 [版本 &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)   
 [商務規則 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [根據商務規則驗證特定成員 &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
  
