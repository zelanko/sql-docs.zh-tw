---
title: 將權限授與使用者及警示管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 166808e1-ada7-48d2-bda8-8f7c017fb3aa
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 829b1bd5069dd8fbeb3c2762d19e6d2d9e3f892d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036089"
---
# <a name="grant-permissions-to-users-and-alerting-administrators"></a>將權限授與使用者及警示管理員
  使用者和警示系統管理員必須經過 SharePoint 權限的授與，才能建立、編輯、刪除及檢視資料警示。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料警示功能沒有特殊權限可供使用，您需使用內建的 SharePoint 權限。  
  
 **資訊工作者** - 權限必須包含「建立警示」和「檢視項目」的 SharePoint 權限。 名稱為「設計」、「參與」、「讀取」及「僅檢視」的內建 SharePoint 權限等級包含「建立警示」和「檢視項目」的 SharePoint 權限。 您也可以使用支援使用者建立、編輯、執行及檢視資料警示所需的權限，建立自訂權限等級。  
  
 **警示系統管理員** - 權限必須包含「管理警示」的 SharePoint 權限。 根據預設，只有「完整控制權」權限層級包含使用「小組網站」網站範本建立的這項網站權限。 如果您使用其他網站範本，則會看見不同的預設 SharePoint 群組清單。 您可以使用支援警示系統管理員檢視及刪除資料警示所需的權限，將「管理警示」權限加入其中一個內建權限等級或建立自訂權限等級。  
  
 若要深入了解 SharePoint 權限，請參閱 [使用者權限與權限等級 (SharePoint Server 2010)](https://technet.microsoft.com/library/cc721640.aspx)。  
  
### <a name="to-grant-permissions"></a>授與權限  
  
1.  移至您要授與權限的 SharePoint 網站。  
  
2.  在工具列上，按一下 **[網站動作]** ，然後按一下 **[網站權限]**。  
  
     如果沒有看到此選項，表示您沒有足夠的權限以將權限授與給其他人。  
  
3.  按一下 **[授與權限]**。  
  
4.  在 [使用者/群組] 中，輸入要授與權限的使用者名稱、群組名稱或電子郵件地址。  
  
5.  選取 **[加入使用者至 SharePoint 群組]** 或 **[直接授與使用者權限]** 選項。 根據您選取的是 **[新增使用者至 SharePoint 群組]** 或是 **[直接授與使用者權限]** 而定，執行下列其中一項操作：  
  
    -   如果您選取了 [新增使用者至 SharePoint 群組]，請選取下拉式清單中的權限等級。  
  
    -   如果您選取了 **[直接授與使用者權限]**，請選取權限等級。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [設定 SharePoint 網站上報表伺服器項目的權限 &#40;SharePoint 整合模式的 Reporting Services&#41;](security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services Data Alerts](../ssms/agent/alerts.md)  
  
  
