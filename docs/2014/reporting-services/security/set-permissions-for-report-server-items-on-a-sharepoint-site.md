---
title: 設定 SharePoint 網站上報表伺服器專案的許可權（SharePoint 整合模式中的 Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
ms.assetid: 2467c657-a3bf-4ec3-a88c-8877df19823d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9c8c0e8f0714efb337d78d4440938dcb5a332fcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101557"
---
# <a name="set-permissions-for-report-server-items-on-a-sharepoint-site-reporting-services-in-sharepoint-integrated-mode"></a>設定 SharePoint 網站上報表伺服器項目的權限 (SharePoint 整合模式的 Reporting Services)
  如果預設安全性設定無法提供所需的存取層級，您可以建立新的權限等級，以便提供特定報表伺服器項目或作業的存取權。 如果您想要限制特定報表的存取權，自訂安全性設定就很有用。  
  
 您必須是網站擁有者才能建立權限等級和群組。 權限等級適用於網站全域。 如果您建立新的權限等級，其他網站擁有者都可以使用該權限等級。  
  
 大部分權限是繼承自上層網站。 如果您為特定文件庫或項目指派權限，就會中斷權限繼承，並且在網站階層中該分支的權限管理方面產生額外的負擔。  
  
 您還可以在報表定義 (.rdl)、模型 (.smdl) 及共用資料來源 (.rsds) 檔上設定權限。 不過您無法組合相同項目上的繼承和管理權限。 如果您選擇直接管理權限，則繼承權限對於目前項目將不會有作用。 如果之後要恢復權限繼承，您可以在 **[動作]** 功能表上選取 **[繼承權限]** 。  
  
 若要設定模型中實體和檢視方塊的權限，您必須具有該模型的「完整控制權」權限等級。 「完整控制權」包括「管理權限」，這個網站層級權限會授與具有「完整控制權」權限等級的網站擁有者和其他 SharePoint 群組。 如果要提供設定模型項目安全性的功能給特定使用者，就必須中斷權限繼承，並針對模型檔授與使用者或群組更高的權限 (例如「完整控制權」)。 當您針對文件庫中的項目 (例如檔案) 授與「完整控制權」時，這些權限的範圍僅限於該項目，不會擴充至父代或相同文件庫中的其他項目。 在使用者具有模型的「管理權限」之後，該使用者就可以透過 SharePoint 網站或模型設計師使用設定模型項目安全性。  
  
### <a name="to-set-permissions-on-an-individual-report-model-or-data-source"></a>設定個別報表、模型或資料來源的權限  
  
1.  如果尚未開啟文件庫，請按一下 [快速啟動] 上的文件庫名稱。 如果找不到您的文件庫名稱，請先按一下 **[檢視所有網站內容]** ，然後再按一下文件庫名稱。  
  
2.  指向報表、報表模型或共用資料來源檔。  
  
3.  按一下向下箭頭，然後在功能表上按一下 **[管理權限]** 。  
  
4.  在 **[動作]** 功能表上，按一下 **[編輯權限]** ，然後按一下 **[確定]** 確認該動作。  
  
5.  若要將權限授與尚未具備該檔案使用權限的使用者或群組，請按一下 **[新增]** ，然後按一下 **[加入使用者]** 。  
  
6.  若要移除或修改現有使用者或群組的權限，請按一下使用者或群組旁的核取方塊，並按一下 **[動作]** ，然後按一下 **[移除使用者權限]** 或 **[編輯使用者權限]** 。  
  
### <a name="to-set-permissions-that-enable-model-item-security"></a>設定啟用模型項目安全性的權限  
  
1.  使用在網站上具有「管理權限」的帳戶，登入 SharePoint 網站。  
  
2.  開啟包含模型的文件庫。  
  
3.  指向模型。  
  
4.  按一下模型旁的向下箭頭，然後按一下 **[管理權限]** 。  
  
5.  按一下 **[動作]** 。  
  
6.  按一下 **[編輯權限]** 。 按一下 [確定]  。  
  
7.  按一下 **[新增]** 。  
  
8.  按一下 [加入使用者]  。  
  
9. 在 [使用者/群組] 中，輸入使用者帳戶。  
  
10. 選取 **[直接授與使用者權限]** 。  
  
11. 按一下 **[完整控制權]** 。  
  
12. 按一下 [確定]  。 使用者一旦具有管理特定模型權限的能力，就可以開啟該模型，編輯該模型內的權限。  
  
## <a name="see-also"></a>另請參閱  
 [在 Windows SharePoint Services 中使用報表伺服器項目的內建安全性](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)   
 [設定 SharePoint Web 應用程式中報表伺服器作業的權限](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [報表伺服器項目的 SharePoint 網站和清單權限參考](sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
