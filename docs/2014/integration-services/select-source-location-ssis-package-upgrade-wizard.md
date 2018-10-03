---
title: 選取來源位置 （SSIS 封裝升級精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectsourcelocation.f1
ms.assetid: 429f146e-edb4-4401-a225-f2c8468971c5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7d553bd07dd72ec136c5ec449f67b84dea2d6c57
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228532"
---
# <a name="select-source-location-ssis-package-upgrade-wizard"></a>選取來源位置 (SSIS 封裝升級精靈)
  使用 **[選取來源位置]** 頁面，指定升級封裝的來源。  
  
> [!NOTE]  
>  只有當您從 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或命令提示字元執行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 封裝升級精靈時，才可使用此頁面。  
  
 **執行 SSIS 封裝升級精靈**  
  
-   [使用 SSIS 套件升級精靈來升級 Integration Services 套件](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>靜態選項  
 **封裝來源**  
 選取包含要升級之封裝的儲存位置。 這個選項的值列於下表中。  
  
|值|描述|  
|-----------|-----------------|  
|**[File System]**|指示要升級的封裝位於本機電腦的資料夾中。<br /><br /> 若要讓精靈在升級這些封裝之前先備份原始封裝，原始封裝必須儲存在檔案系統中。 如需詳細資訊，請參閱「如何」主題。|  
|**SSIS 封裝存放區**|指示要升級的封裝位於封裝存放區中。 此封裝存放區是由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所管理的檔案系統資料夾集合所組成。 如需詳細資訊，請參閱 [AllMembers &#40;MDX&#41;](service/package-management-ssis-service.md)。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
|**Microsoft SQL Server**|指示要升級的封裝是來自現有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
  
 **資料夾**  
 輸入包含您想要升級之封裝的資料夾名稱，或是按一下 [瀏覽] 並尋找資料夾。  
  
 **瀏覽**  
 瀏覽來尋找包含您要升級之封裝的資料夾。  
  
## <a name="package-source-dynamic-options"></a>封裝來源動態選項  
  
### <a name="package-source--ssis-package-store"></a>封裝來源 = SSIS 封裝存放區  
 **Server**  
 輸入具有要升級之封裝的伺服器名稱，或是從清單中選取此伺服器。  
  
### <a name="package-source--microsoft-sql-server"></a>封裝來源 = Microsoft SQL Server  
 **Server**  
 輸入具有要升級之封裝的伺服器名稱，或是從清單中選取此伺服器。  
  
 **使用 Windows 驗證**  
 選取此選項可使用 Windows 驗證來連接伺服器。  
  
 **使用 SQL Server 驗證**  
 選取此選項可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證連接到伺服器。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證將用來連接伺服器的使用者名稱。  
  
 **密碼**  
 輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證將用來連接伺服器的密碼。  
  
## <a name="see-also"></a>另請參閱  
 [升級 Integration Services 套件](install-windows/upgrade-integration-services-packages.md)  
  
  
