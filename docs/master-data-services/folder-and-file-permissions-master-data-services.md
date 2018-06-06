---
title: 資料夾和檔案權限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], file and folder
- folders [Master Data Services]
- files [Master Data Services]
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b4460ef0b2c620bbfe97a69d04f23e63dde04cea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="folder-and-file-permissions-master-data-services"></a>資料夾和檔案的權限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  當您安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]時，資料夾和檔案會安裝在檔案系統中針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 共用功能所指定的安裝路徑。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 共用功能的預設安裝路徑， [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 的安裝路徑為 *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services。 雖然您可以變更共用功能的安裝路徑，但請注意繼承自父資料夾的權限以及為 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]明確設定的權限。  
  
## <a name="inherited-permissions"></a>繼承的權限  
 **Microsoft SQL Server** 資料夾、 **Master Data Services** 資料夾，以及大部分子資料夾和檔案都會從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式中指定的父資料夾繼承權限。 如果您選擇預設安裝位置，則會從下列父資料夾繼承權限： *drive*:\Program Files。 下表描述 **Program Files**的預設權限。  
  
> [!NOTE]  
>  如果您修改 **Program Files**的預設權限或選擇不同的安裝位置， [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料夾和檔案會跟著從其父資料夾繼承權限，而這些權限可能不同於下表所描述的權限。  
  
###### <a name="program-files-default-permissions"></a>Program Files 的預設權限  
  
|群組或帳戶名稱|Permissions|  
|---------------------------|-----------------|  
|CREATOR OWNER|特殊權限|  
|SYSTEM|特殊權限|  
|系統管理員|特殊權限|  
|使用者|讀取與執行、列出資料夾內容、讀取|  
|TrustedInstaller|列出資料夾內容、特殊權限|  
  
## <a name="explicit-permissions"></a>明確權限  
 **MDSTempDir** 資料夾和 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config 檔案 (在 **WebApplication** 資料夾中) 不會繼承權限。 它們的權限是在您安裝 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]時明確設定，無論所選安裝路徑為何。 請不要修改這些權限。  
  
###### <a name="mdstempdir-permissions"></a>MDSTempDir 的權限  
  
|群組或帳戶名稱|Permissions|  
|---------------------------|-----------------|  
|SYSTEM|修改、讀取與執行、列出資料夾內容、讀取、寫入|  
|系統管理員|修改、讀取與執行、列出資料夾內容、讀取、寫入|  
|MDS_ServiceAccounts|修改、讀取與執行、列出資料夾內容、讀取、寫入|  
  
###### <a name="webconfig-permissions"></a>Web.config 的權限  
  
|群組或帳戶名稱|Permissions|  
|---------------------------|-----------------|  
|SYSTEM|完全控制、修改、讀取與執行、讀取、寫入|  
|系統管理員|完全控制、修改、讀取與執行、讀取、寫入|  
|MDS_ServiceAccounts|讀取與執行、讀取|  
  
 如需 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config 檔案內容的詳細資訊，請參閱 [Web 組態參考 &#40;Master Data Services&#41;](../master-data-services/web-configuration-reference-master-data-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Master Data Services](../master-data-services/install-windows/install-master-data-services.md)  
  
  
