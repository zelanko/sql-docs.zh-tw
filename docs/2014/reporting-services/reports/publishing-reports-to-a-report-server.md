---
title: 將報表發行至報表伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 135a736f6d0cf0cd5c51cf40b05c95a33d5c435b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128614"
---
# <a name="publishing-reports-to-a-report-server"></a>將報表發行至報表伺服器
  在您設計和測試完報表或報表集之後，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的內建部署功能，將報表發行至實際報表伺服器。 您可以發行個別的報表或報表伺服器專案。 發行報表伺服器專案是發行多份報表最簡單的方式。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用這個詞彙*部署*，而不是一詞*發佈*。 這兩個詞可以互換。  
  
 在您發行報表之前，您必須具有可執行此動作的權限。 權限是透過由您報表伺服器管理員所定義的角色安全性所決定。 發佈作業一般是透過「發行者」角色授與。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會提供專案組態來管理報表發行。 組態會指定報表伺服器的位置、報表伺服器上所安裝之 SQL Server Reporting Services 的版本、是否覆寫發行到報表伺服器的資料來源等等。 除了使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 所提供的組態，您還可以建立其他組態。  
  
## <a name="project-configurations"></a>專案組態  
 報表會在發行前建立，以確保只有有效的報表定義會發行到報表伺服器。 專案組態包括建立報表的屬性，例如，暫時儲存已建立之報表的資料夾，以及如何處理建立問題。 組態也包含您用來指定報表伺服器之位置與版本、報表伺服器上之資料夾的屬性。  
  
 根據預設，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]提供三種專案組態：DebugLocal、 Debug 與 Release。 預設組態為 DebugLocal。 您通常可以使用 DebugLocal 組態在本機預覽視窗中檢視報表、使用 Debug 組態將報表發行至測試伺服器，以及使用 Release 組態將報表發行至實際伺服器。 在標準工具列上的方案組態下拉式清單中會顯示使用中的組態。 若要使用不同的組態，請從清單中進行選取。  
  
 您的報表環境可能已安裝多部報表伺服器以及不同版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 您可以建立多個組態，然後根據部署狀況，使用不同的組態。 如需詳細資訊，請參閱 <<c0> [ 部署和版本支援 SQL Server Data Tools 中&#40;SSRS&#41; ](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)並[設定部署屬性&#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)。</c0>  
  
## <a name="publishing-reports"></a>發行報表  
 您可以發行單一報表或包含多個報表的報表伺服器專案。 如需有關發行報表的指示，請參閱[發行的報表](../publish-reports.md)。  
  
### <a name="publishing-a-single-report"></a>發行單一報表  
 如果您不要發行專案中的所有報表，可以只選擇發行單一報表。 若要這樣做，請選取部署報表的設定 (例如 Release 設定)，以滑鼠右鍵按一下報表，然後按一下 [部署]。  
  
 如果報表使用共用資料來源，您也必須部署共用資料來源，否則將不會執行部署的報表。 以滑鼠右鍵按一下共用資料來源，然後按一下 [部署]。  
  
 您必須指定報表伺服器的目標伺服器 URL，並視需要變更負責部署報表和共用資料來源的預設資料夾。  
  
### <a name="publishing-multiple-reports"></a>發行多個報表  
 當您發行報表伺服器專案時，您可以發行該專案中的所有報表。 所有報表都可以使用相同的報表組態，部署至相同的報表伺服器、伺服器上相同的資料夾等等。 若要將報表發行至不同的伺服器，請逐個報表發行，或僅包含報表伺服器專案中您要發行的報表。 一個方案可以包含多個報表伺服器專案，而且，使用多個專案可能會讓報表部署的管理更為容易，因為您可以使用不同的組態部署不同的專案。  
  
## <a name="see-also"></a>另請參閱  
 [專案屬性頁對話方塊](../tools/project-property-pages-dialog-box.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [升級報表](../install-windows/upgrade-reports.md)  
  
  
