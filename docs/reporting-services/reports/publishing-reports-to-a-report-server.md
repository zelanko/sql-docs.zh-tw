---
title: 將報表發行至報表伺服器 | Microsoft Docs
ms.date: 06/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- production environments [Reporting Services]
- report projects [Reporting Services]
- Debug configuration [Reporting Services]
- report publishing [Reporting Services]
- publishing reports [Reporting Services]
- report properties [Reporting Services]
- Report Designer [Reporting Services], deploying reports
- Production configuration [Reporting Services]
- publishing reports [Reporting Services], production environments
- DebugLocal configuration [Reporting Services]
- deploying [Reporting Services], reports
- Report Designer [Reporting Services], publishing reports
ms.assetid: bd7aa5e0-61ce-43fd-8f74-5d1aeed078bb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 44d376414ce4043bca6f053c6523365af5d96d4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47714102"
---
# <a name="publishing-reports-to-a-report-server"></a>將報表發行至報表伺服器
  在您設計和測試完報表或報表集之後，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的部署功能，將報表發行至報表伺服器。 您可以發行個別報表，或可包含多個報表和資料來源的報表伺服器專案。 發行報表伺服器專案是發行多份報表最簡單的方式。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用「部署」一詞，而不是「發行」一詞。 這兩個詞可以互換。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會提供專案組態來管理報表發行。 組態會指定報表伺服器的位置、報表伺服器上所安裝之 SQL Server Reporting Services 的版本、是否覆寫發行到報表伺服器的資料來源等等。 例如，"Debug" 組態可以發行至與 "Release" 組態不同的伺服器。 除了使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 所提供的組態，您還可以建立其他組態。  
 
## <a name="requirements-to-publish"></a>發行需求
權限是透過由您報表伺服器管理員所定義的角色安全性所決定。 發行作業一般是透過 **發行者角色**授與。  
  
## <a name="project-configurations"></a>專案組態  
 您的報表環境可能已安裝多部報表伺服器以及不同版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 您可以建立多個組態，然後根據部署狀況，使用不同的組態。 專案組態包括建立報表的屬性，例如，暫時儲存已建立之報表的資料夾，以及如何處理建立問題。 組態也包含您用來指定報表伺服器之位置與版本、報表伺服器上之資料夾的屬性。  
  
 根據預設， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 提供三種專案組態： **DebugLocal**、 **Debug**與 **Release**。 預設組態為 DebugLocal。 您通常可以使用 DebugLocal 組態在本機預覽視窗中檢視報表、使用 Debug 組態將報表發行至測試伺服器，以及使用 Release 組態將報表發行至實際伺服器。 在標準工具列上的方案組態下拉式清單中會顯示使用中的組態。 若要使用不同的組態，請從清單中進行選取。  
  
 ![ssrs_project_properties](../../reporting-services/reports/media/ssrs-project-properties.png) 
  
 如需詳細資訊，請參閱下列內容
 + [專案屬性頁對話方塊](../../reporting-services/tools/project-property-pages-dialog-box.md)
 + [SQL Server 資料工具中的部署和版本支援](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)
 + [在 SSDT 中設定 Reporting Services 專案的部署屬性](../../reporting-services/tools/set-deployment-properties-reporting-services.md)
  
## <a name="to-publish-all-reports-in-a-project"></a>若要發行專案中的所有報表  
  
在 [組建] 功能表上，按一下 [部署 \<報表專案名稱>]。 或者，在方案總管中，以滑鼠右鍵按一下報表專案，然後按一下 [部署]。 您可以在 [輸出] 視窗中，檢視發行程序的狀態。  
  
當您部署報表伺服器專案時，也會部署報表專案中的共用資料來源。 所有報表都可以使用相同的報表組態，部署至相同的報表伺服器、伺服器上相同的資料夾等等。 若要將報表發行至不同的伺服器，請逐個報表發行，或僅包含報表伺服器專案中您要發行的報表。 一個方案可以包含多個報表伺服器專案，而且，使用多個專案可能會讓報表部署的管理更為容易，因為您可以使用不同的組態部署不同的專案。 
  
## <a name="to-publish-a-single-report"></a>若要發行單一報表  
  
在 [方案總管] 中，以滑鼠右鍵按一下報表，然後按一下 **[部署]**。 您可以在 [輸出] 視窗中，檢視發行程序的狀態。  
  
 當您發行報表時，也必須部署該報表所使用的共用資料來源。   
 如果您不要發行專案中的所有報表，可以只選擇發行單一報表。 若要這樣做，請選取部署報表的設定 (例如 Release 設定)，以滑鼠右鍵按一下報表，然後按一下 [部署]。  
  
 如果報表使用共用資料來源，您也必須部署共用資料來源，否則將不會執行部署的報表。 以滑鼠右鍵按一下共用資料來源，然後按一下 [部署]。  
  
 您必須指定報表伺服器的目標伺服器 URL，並視需要變更負責部署報表和共用資料來源的預設資料夾。  

  
## <a name="see-also"></a>另請參閱  
 [專案屬性頁對話方塊](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [升級報表](../../reporting-services/install-windows/upgrade-reports.md)  
  
  
