---
title: 建立 Web 應用程式對話方塊 (Master Data Services 組態管理員) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: dac7b74969c341b7f68c7dfbf56d2314d9ab4427
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788360"
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>建立 Web 應用程式對話方塊 (Master Data Services 組態管理員)
  使用 [建立 Web 應用程式] 對話方塊可建立 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。 這個 Web 應用程式會建立在您於 [Web 組態] 頁面上所選取的網站中。  
  
## <a name="web-application"></a>Web 應用程式  
 Web 伺服器會針對檔案系統中， [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** 資料夾內的這個 Web 應用程式提供內容。 這個位置指定在安裝期間，而且預設路徑是*磁碟機*: \Program Files\Microsoft SQL Server\120\Master Data Services\WebApplication。  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|虛擬路徑|選取您想要建立 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式的虛擬路徑。 虛擬路徑是用來存取 Web 應用程式之 URL 的一部分。<br /><br /> 這個清單會經過篩選，只顯示可以建立 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式的應用程式虛擬路徑。 您無法在另一個 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式底下建立 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式。|  
|別名|輸入 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式的名稱，或使用預設名稱。 這個名稱會在 URL 中用來從 Web 瀏覽器存取 Web 應用程式。|  
  
## <a name="application-pool"></a>應用程式集區  
  
|控制項名稱|描述|  
|------------------|-----------------|  
|**名稱**|請輸入新應用程式集區的唯一易記名稱，或使用預設名稱。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式會新增至這個應用程式集區。<br /><br /> 應用程式集區提供了界限，可防止一個應用程式集區中的應用程式影響另一個應用程式集區中的應用程式。|  
|**使用者名稱**|輸入 Active Directory 中的網域和使用者名稱。 此帳戶是 Web 應用程式在其中執行之應用程式集區的識別。 這個帳戶應該與建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 時指定為服務帳戶的帳戶相同。<br /><br /> 這個帳戶會加入至 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫的 mds_exec 資料庫角色，來進行資料庫存取。 如需詳細資訊，請參閱[資料庫登入、使用者和角色 &#40;Master Data Services&#41;](database-logins-users-and-roles-master-data-services.md)。 它也會新增至 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Windows 群組 (**MDS_ServiceAccounts**)，而這個群組在檔案系統中已被授與暫存編譯目錄 **MDSTempDir** 的權限。 如需詳細資訊，請參閱[資料夾和檔案的權限 &#40;Master Data Services&#41;](../../2014/master-data-services/folder-and-file-permissions-master-data-services.md)。|  
|**密碼**|輸入指定之使用者帳戶的密碼。|  
|**確認密碼**|重新輸入指定之使用者帳戶的密碼。 **[密碼]** 和 **[確認密碼]** 欄位必須包含相同的密碼。|  
  
## <a name="see-also"></a>另請參閱  
 [Web 組態頁面 &#40;Master Data Services 組態管理員&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
 [設定 Master Data Services 資料庫和網站](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Web 應用程式需求&#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [建立主資料管理員 Web 應用程式 &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
