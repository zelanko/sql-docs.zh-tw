---
title: 變更系統管理員帳戶（Master Data Services） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 911bd20c7d232bca52fdf9dca294bd7a4924d984
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054142"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>變更系統管理員帳戶 (Master Data Services)
  您可以變更指定為[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]系統管理員的使用者帳戶。  
  
> [!WARNING]  
>  當您完成這個程序時，先前的系統管理員使用者帳戶會遭到刪除。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須將新的系統管理員使用者名稱加入 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者清單。 如需詳細資訊，請參閱[Add a User &#40;Master Data Services&#41;](add-a-user-master-data-services.md)。  
  
-   您必須在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中擁有檢視 mdm.tblUser 及執行 mdm.udpSecurityMemberProcessRebuildModel 預存程序的權限。 如需詳細資訊，請參閱[資料庫物件安全性 &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md)。  
  
### <a name="to-change-the-administrator-account"></a>若要變更系統管理員帳戶  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並且連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體。  
  
2.  在 [tblUser] 中，尋找將成為新系統管理員的使用者，並複製資料`SID`行中的值。  
  
3.  建立新的查詢。  
  
4.  輸入下列文字，以新的系統管理員的使用者名稱和*SID*取代*DOMAIN \ user_name* ，並使用您在步驟2中複製的值。  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  執行查詢。  
  
## <a name="see-also"></a>另請參閱  
 [管理員 &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
  
