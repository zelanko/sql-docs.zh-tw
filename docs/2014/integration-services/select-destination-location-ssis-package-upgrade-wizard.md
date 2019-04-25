---
title: 選取目的地位置 （SSIS 封裝升級精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectdestinationlocation.f1
ms.assetid: 89274a71-0ffe-4889-84df-f5a7d78459ef
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 167e8deb4009e7bf9398f89665cad9b3d368b1eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766640"
---
# <a name="select-destination-location-ssis-package-upgrade-wizard"></a>選取目的地位置 (SSIS 封裝升級精靈)
  使用 **[選取目的地位置]** 頁面，指定用來儲存升級封裝的目的地。  
  
> [!NOTE]  
>  只有當您從 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或命令提示字元執行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 封裝升級精靈時，才可使用此頁面。  
  
 **執行 SSIS 封裝升級精靈**  
  
-   [使用 SSIS 套件升級精靈來升級 Integration Services 套件](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>靜態選項  
 **儲存至來源位置**  
 將升級封裝儲存到此精靈之 [選取來源位置] 頁面上所指定的相同位置。  
  
 如果原始封裝儲存在檔案系統中，而且您希望精靈備份這些封裝，請選取 **[儲存至來源位置]** 選項。 如需詳細資訊，請參閱 [使用 SSIS 封裝升級精靈來升級 Integration Services 封裝](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
 **選取新的目的地位置**  
 將升級封裝儲存到此頁面上指定的目的地位置。  
  
 **封裝來源**  
 指定要儲存升級封裝的位置。 這個選項的值列於下表中。  
  
|值|描述|  
|-----------|-----------------|  
|**[File System]**|指示升級封裝要儲存到本機電腦的資料夾中。|  
|**SSIS 封裝存放區**|指示升級封裝要儲存到 Integration Services 封裝存放區。 此封裝存放區是由 Integration Services 服務所管理的檔案系統資料夾集合所組成。 如需詳細資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](service/package-management-ssis-service.md)。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
|**Microsoft SQL Server**|指示升級封裝要儲存到現有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
  
 **資料夾**  
 輸入將用來儲存升級封裝的資料夾名稱，或是按一下 [瀏覽] 並尋找資料夾。  
  
 **瀏覽**  
 瀏覽來尋找將儲存升級封裝的資料夾。  
  
## <a name="package-source-dynamic-options"></a>封裝來源動態選項  
  
### <a name="package-source--ssis-package-store"></a>封裝來源 = SSIS 封裝存放區  
 **Server**  
 輸入升級封裝儲存所在的伺服器名稱，或是從清單中選取伺服器。  
  
### <a name="package-source--microsoft-sql-server"></a>封裝來源 = Microsoft SQL Server  
 **Server**  
 輸入升級封裝儲存所在的伺服器名稱，或是從清單中選取此伺服器。  
  
 **使用 Windows 驗證**  
 選取此選項可使用 Windows 驗證來連接伺服器。  
  
 **使用 SQL Server 驗證**  
 選取此選項可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證連接到伺服器。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 輸入使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證來連接伺服器時所要使用的使用者名稱。  
  
 **密碼**  
 輸入使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證來連接伺服器時所要使用的密碼。  
  
## <a name="see-also"></a>另請參閱  
 [升級 Integration Services 封裝](install-windows/upgrade-integration-services-packages.md)  
  
  
