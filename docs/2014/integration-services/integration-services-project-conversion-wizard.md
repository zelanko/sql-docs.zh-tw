---
title: Integration Services 專案轉換向導 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.migrationwizard.f1
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9c077fdb85612c5e3f574d9d0236b07f149b9c3a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057981"
---
# <a name="integration-services-project-conversion-wizard"></a>Integration Services 專案轉換精靈
  [Integration Services 專案轉換精靈]**** 會將專案轉換為專案部署模型。  
  
> [!NOTE]  
>  如果專案包含一個或多個資料來源，則在完成專案轉換時，會移除資料來源。 若要在專案中建立可以透過封裝共用的資料來源連接，請在專案層級加入連接管理員。 如需詳細資訊，請參閱 [加入、刪除或共用封裝中的連線管理員](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)。  
  
 **您想要做什麼事？**  
  
-   [開啟 [Integration Services 專案轉換精靈]](#open_dialog)  
  
-   [設定 [尋找封裝] 頁面上的選項](#locate)  
  
-   [設定 [選取封裝] 頁面上的選項](#selectPackages)  
  
-   [設定 [選取目的地] 頁面上的選項](#destination)  
  
-   [設定 [指定專案屬性] 頁面上的選項](#projectProperties)  
  
-   [設定 [更新執行封裝工作] 頁面上的選項](#executePackage)  
  
-   [在 [選取設定] 頁面上設定選項](#configurations)  
  
-   [設定 [建立參數] 頁面上的選項](#createParameters)  
  
-   [設定 [設定參數] 頁面上的選項](#configureParameters)  
  
-   [設定 [檢閱] 頁面上的選項](#review)  
  
-   [設定 [執行轉換] 上的選項](#conversion)  
  
##  <a name="open-the-integration-services-project-conversion-wizard"></a><a name="open_dialog"></a>開啟 Integration Services 專案轉換向導  
 執行下列其中一項作業來開啟 [Integration Services 專案轉換精靈]****。  
  
-   開啟 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的專案，然後在方案總管中，以滑鼠右鍵按一下該專案，並按一下 [轉換為專案部署模型]****。  
  
-   從 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 的物件總管中，以滑鼠右鍵按一下 [專案]**** 節點，然後選取 [匯入封裝]****。  
  
 根據您是從 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 還是從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行 [Integration Services 專案轉換精靈]****，此精靈會執行不同的轉換工作。 如需詳細資訊，請參閱 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
##  <a name="set-options-on-the-locate-packages-page"></a><a name="locate"></a>設定 [尋找封裝] 頁面上的選項  
  
> [!NOTE]  
>  只有在您從 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 執行此精靈時，才可以使用 [尋找封裝]**** 頁面。  
  
 當您選取 [來源]**** 下拉式清單中的 [檔案系統]**** 時，下列選項會顯示在頁面上。 當封裝位於檔案系統時，請選取此選項。  
  
 **資料夾**  
 輸入封裝路徑，或按一下 [瀏覽]**** 巡覽到封裝。  
  
 當您選取 [來源]**** 下拉式清單中的 [SSIS 封裝存放區]**** 時，下列選項會顯示在頁面上。 如需封裝存放區的詳細資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](service/package-management-ssis-service.md)。  
  
 **Server**  
 輸入伺服器名稱，選取伺服器。  
  
 **資料夾**  
 輸入封裝路徑，或按一下 [瀏覽]**** 巡覽到封裝。  
  
 當您選取 [來源]**** 下拉式清單中的 [Microsoft SQL Server]**** 時，下列選項會顯示在頁面上。 當封裝位於 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]時，請選取此選項。  
  
 **Server**  
 輸入伺服器名稱，選取伺服器。  
  
 **使用 Windows 驗證**  
 Microsoft Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。 如果您使用 Windows 驗證，就不需要提供使用者名稱或密碼。  
  
 **使用 SQL Server 驗證**  
 當使用者透過不信任連接並指定登入名稱和密碼進行連接時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會驗證此連接，檢查是否已建立該 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入帳戶，而且指定的密碼是否符合先前記錄的密碼。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。  
  
 **使用者名稱**  
 使用 SQL Server 驗證時，請指定使用者名稱。  
  
 **密碼**  
 使用 SQL Server 驗證時，請提供密碼。  
  
 **資料夾**  
 輸入封裝路徑，或按一下 [瀏覽]**** 巡覽到封裝。  
  
##  <a name="set-options-on-the-select-packages-page"></a><a name="selectPackages"></a>設定 [選取封裝] 頁面上的選項  
 **封裝名稱**  
 列出封裝檔案。  
  
 **狀態**  
 指出封裝是否就緒，可以轉換成專案部署模型。  
  
 **訊息**  
 顯示與封裝相關聯的訊息。  
  
 **密碼**  
 顯示與封裝相關聯的密碼。 密碼文字是隱藏的。  
  
 **套用至選取項目**  
 按一下可將 [密碼]**** 文字方塊中的密碼套用至選取的一個或多個封裝。  
  
 **重新整理**  
 重新整理封裝的清單。  
  
##  <a name="set-options-on-the-select-destination-page"></a><a name="destination"></a>設定 [選取目的地] 頁面上的選項  
 在此頁面上，指定新專案部署檔案 (.ispac) 的名稱和路徑，或選取現有的檔案。  
  
> [!NOTE]  
>  只有在您從 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 執行此精靈時，才可以使用 [選取目的地]**** 頁面。  
  
 **輸出路徑**  
 輸入部署檔案的路徑，或按一下 [瀏覽]**** 巡覽到檔案。  
  
 **專案名稱**  
 輸入專案名稱。  
  
 **保護等級**  
 選取保護等級。 如需詳細資訊，請參閱 [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)。  
  
 **專案描述**  
 選擇性地輸入專案的描述。  
  
##  <a name="set-options-on-the-specify-project-properties-page"></a><a name="projectProperties"></a>設定 [指定專案屬性] 頁面上的選項  
  
> [!NOTE]  
>  只有在您從 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 執行此精靈時，才可以使用 [指定專案屬性]**** 頁面。  
  
 **專案名稱**  
 列出專案名稱。  
  
 **保護等級**  
 選取專案中包含之封裝的保護等級。 如需保護等級的詳細資訊，請參閱 [封裝中的敏感性資料存取控制](security/access-control-for-sensitive-data-in-packages.md)。  
  
 **專案描述**  
 選擇性地輸入專案描述。  
  
##  <a name="set-options-on-the-update-execute-package-task-page"></a><a name="executePackage"></a>設定 [更新執行封裝工作] 頁面上的選項  
 更新執行封裝工作包含在封裝中，以使用專案參考。 如需詳細資訊，請參閱＜ [執行封裝工作編輯器](../../2014/integration-services/execute-package-task-editor.md)＞。  
  
 **父封裝**  
 列出使用「執行封裝」工作執行子封裝之封裝的名稱。  
  
 **工作名稱**  
 列出「執行封裝」工作的名稱。  
  
 **原始參考**  
 列出子封裝的目前路徑。  
  
 **指派參考**  
 選取專案中儲存的子封裝。  
  
##  <a name="set-options-on-the-select-configurations-page"></a><a name="configurations"></a> 設定 [選取組態] 頁面上的選項  
 選取您要以參數取代的封裝組態。  
  
 **套件**  
 列出封裝檔案。  
  
 **類型**  
 列出組態類型，例如 XML 組態檔。  
  
 **組態字串**  
 列出組態檔的路徑。  
  
 **狀態**  
 顯示組態的狀態訊息。 按一下訊息可檢視完整訊息文字。  
  
 **加入組態**  
 將其他專案中包含的封裝組態加入至您要以參數取代的可用組態清單中。 您可以選取儲存在檔案系統或 SQL Server 中的組態。  
  
 **重新整理**  
 按一下可重新整理組態的清單。  
  
 **轉換後從所有封裝移除組態**  
 建議您選取此選項以便從專案中移除所有組態。  
  
 如果您沒有選取此選項，則只會移除您選擇以參數取代的組態。  
  
##  <a name="set-options-on-the-create-parameters-page"></a><a name="createParameters"></a> 設定 [建立參數] 頁面上的選項  
 選取每個組態屬性的參數名稱和範圍。  
  
 **套件**  
 列出封裝檔案。  
  
 **參數名稱**  
 列出參數名稱。  
  
 **範圍**  
 選取參數的範圍 (封裝或專案)。  
  
##  <a name="set-options-on-the-configure-parameters-page"></a><a name="configureParameters"></a>設定 [設定參數] 頁面上的選項  
 **名稱**  
 列出參數名稱。  
  
 **範圍**  
 列出參數的範圍。  
  
 **ReplTest1**  
 列出參數值。  
  
 按一下值欄位旁邊的省略符號按鈕來設定參數屬性。  
  
 在 [設定參數詳細資料]**** 對話方塊中，您可以編輯參數值。 您也可以指定在執行封裝時是否必須提供此參數值。  
  
 您可以按一下參數旁邊的瀏覽按鈕，在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 之 [設定]**** 對話方塊的 [參數]**** 頁面中修改值。 [設定參數值]**** 對話方塊隨即出現。  
  
 [設定參數詳細資料]**** 對話方塊也會列出參數值的資料類型，以及參數的來源。  
  
##  <a name="set-the-options-on-the-review-page"></a><a name="review"></a>設定 [審查] 頁面上的選項  
 使用 [檢閱]**** 頁面確認您已經針對專案的轉換選取的選項。  
  
 **上一步**  
 按一下可變更選項。  
  
 **將**  
 按一下可將專案轉換為專案部署模型。  
  
##  <a name="set-the-options-on-the-perform-conversion"></a><a name="conversion"></a>設定 [執行轉換] 上的選項  
 [執行轉換] 頁面會顯示專案轉換的狀態。  
  
 **動作**  
 列出特定的轉換步驟。  
  
 **Result**  
 列出每個轉換步驟的狀態。 如需詳細資訊，請按一下狀態訊息。  
  
 在專案儲存到 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中之前，不會儲存專案轉換。  
  
 **儲存報表**  
 按一下可將專案轉換的摘要儲存在 .xml 檔案中。  
  
## <a name="see-also"></a>另請參閱  
 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)  
  
  
