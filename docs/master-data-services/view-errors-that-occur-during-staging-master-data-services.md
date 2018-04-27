---
title: 檢視暫存期間發生的錯誤 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72c22de68a3a07b3f6a21687a7f6d0eae6906d6d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>檢視暫存期間發生的錯誤 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以檢視暫存處理序期間發生的錯誤。 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫提供下列兩個用來顯示錯誤的檢視：  
  
-   分葉或合併成員更新適用的 stg.viw_name_MemberErrorDetails。  
  
-   階層關聯性更新適用的 stg.viw_name_RelationshipErrorDetails。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中，您必須具有 stg.viw_name_MemberErrorDetails 或 stg.viw_name_RelationshipErrorDetails 檢視的 SELECT 權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-view-staging-errors"></a>檢視暫存錯誤  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並且連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體。  
  
2.  開啟新的查詢。  
  
3.  輸入下列文字，以您的暫存資料表名稱取代名稱，例如 viw_Product_MemberErrorDetails。  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  執行查詢。 錯誤詳細資料會顯示在 **ErrorDescription** 欄位中。  
  
## <a name="next-steps"></a>Next Steps  
 如需錯誤訊息的詳細資訊，請參閱[暫存處理序錯誤 &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [概觀：從資料表匯入資料 &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [暫存處理序疑難排解 (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
