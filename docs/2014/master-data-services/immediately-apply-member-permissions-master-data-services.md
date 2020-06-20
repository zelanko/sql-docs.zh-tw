---
title: 立即套用成員權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], applying permissions immediately
- permissions [Master Data Services], applying member permissions immediately
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f76cb9aaf111f17928c8a6afbd2888d62bbc4d91
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971398"
---
# <a name="immediately-apply-member-permissions-master-data-services"></a>立即套用成員權限 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以立即套用成員權限，不等候成員安全性於固定間隔套用。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中擁有執行 mdm.udpSecurityMemberProcessRebuildModel 預存程序的權限。 如需詳細資訊，請參閱[資料庫物件安全性 &#40;Master Data Services&#41;](database-object-security-master-data-services.md)。  
  
### <a name="to-immediately-apply-hierarchy-member-permissions"></a>若要立即套用階層成員權限  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並且連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 資料庫的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 執行個體。  
  
2.  建立新的查詢。  
  
3.  輸入下列文字，以您的資料庫名稱取代 *database* ，並以模型名稱取代 *Model_Name* 。  
  
    ```  
    USE [database];  
    GO  
  
    DECLARE @Model_ID INT;  
    SELECT @Model_ID = ID FROM mdm.tblModel WHERE [Name] = N'Model_Name';  
    EXEC [mdm].[udpSecurityMemberProcessRebuildModel] @Model_ID=@Model_ID, @ProcessNow=1;  
    GO  
    ```  
  
4.  執行查詢。  
  
## <a name="see-also"></a>另請參閱  
 [指派階層成員許可權 &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [階層成員權限 &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
