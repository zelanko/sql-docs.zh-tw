---
title: 建立與表格式模型資料庫的 BI 語義模型連接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 69b306f6-ee8a-44d2-8f51-0cad2c0bc135
author: minewiskan
ms.author: owend
ms.openlocfilehash: 37ce07dd3ae9cbd46a6ddd1860c3178fe154513a
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84535170"
---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>建立與表格式模型資料庫的 BI 語意模型連接
  使用本主題的資訊可設定 BI 語意模型連接，重新導向至 SharePoint 伺服器陣列外部的 Analysis Services 執行個體上執行的表格式模型資料庫。  
  
 在您建立 BI 語意模型連接並且設定 SharePoint 和 Analysis Services 權限之後，人們可以將其當做 Excel 或 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表的資料來源使用。  
  
 本主題包含下列各節。 請依指定順序執行每個工作。  
  
 [檢閱必要條件](#bkmk_prereq)  
  
 [授與 Analysis Services 管理權限給共用服務應用程式](#bkmk_ssas)  
  
 [授與表格式模型資料庫的讀取權限](#bkmk_BISM)  
  
 [建立與表格式模型資料庫的 BI 語義模型連接](#bkmk_connect)  
  
 [設定 BI 語意模型連接的 SharePoint 權限](#bkmk_permissions)  
  
 [後續步驟](#bkmk_next)  
  
##  <a name="review-prerequisites"></a><a name="bkmk_prereq"></a>審查必要條件  
 您必須有 [參與] 以上權限，才能建立 BI 語意模型連接檔案。  
  
 您必須具有支援 BI 語意模型連接內容類型的文件庫。 如需詳細資訊，請參閱[將 BI 語義模型連接內容類型新增至程式庫 &#40;PowerPivot for SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)。  
  
 您必須知道要設定 BI 語意模型連接的伺服器和資料庫名稱。 Analysis Services 必須設定表格式模式。 在伺服器上執行的資料庫必須是表格式模型資料庫。 如需如何檢查伺服器模式的指示，請參閱 [判斷 Analysis Services 執行個體的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
 在某些情況下，SharePoint 環境中的共用服務必須有 Analysis Services 執行個體的管理權限。 這些服務包括 PowerPivot 服務應用程式、Reporting Services 服務應用程式和 PerformancePoint 服務應用程式。 在授與管理權限之前，您必須知道這些服務應用程式的識別。 您可以使用管理中心判斷識別。  
  
 您必須是 SharePoint 服務管理員，才能在管理中心檢視安全性資訊。  
  
 您必須是 Analysis Services 系統管理員，才能在 Management Studio 中授與管理權限。  
  
 PowerPivot for SharePoint 必須透過使用傳統驗證模式的 Web 應用程式來存取。 與外部資料來源的 BI 語意模型連接相依於傳統模式登入。 如需詳細資訊，請參閱[PowerPivot 驗證和授權](power-pivot-authentication-and-authorization.md)。  
  
 參與連接順序的所有電腦和使用者都必須是在相同網域或受信任網域 (雙向信任) 中。  
  
##  <a name="grant-analysis-services-administrative-permissions-to-shared-service-applications"></a><a name="bkmk_ssas"></a>授與 Analysis Services 共用服務應用程式的系統管理許可權  
 從 SharePoint 到 Analysis Services 伺服器上表格式模型資料庫的連接有時是由共用服務代表要求資料的使用者所建立。 發出要求的服務可能是 PowerPivot 服務應用程式、Reporting Services 服務應用程式或 PerformancePoint 服務應用程式。 為了要讓連接成功，此服務必須擁有 Analysis Services 伺服器的管理權限。 在 Analysis Services 中，只允許管理員代表其他使用者建立模擬連接。  
  
 在下列情況下使用連接時需要管理權限：  
  
-   在 BI 語意模型連接檔案的設定期間驗證連接資訊時。  
  
-   當使用 BI 語意模型連接啟動 Power View 報表時。  
  
-   當使用 BI 語意模型連接擴展 PerformancePoint Web 組件時。  
  
 為確保這些行為如預期執行，請將 Analysis Services 執行個體的管理權限授與每個服務識別。 請使用下列指示來授與必要權限。  
  
 **將服務識別加入至伺服器管理員角色**  
  
1.  在 SQL Server Management Studio 中，連接到 Analysis Services 執行個體。  
  
2.  以滑鼠右鍵按一下伺服器名稱，然後選取 **[屬性]**。  
  
3.  按一下 [安全性]****，然後按一下 [加入]****。 輸入用來執行服務應用程式的 Windows 使用者帳戶。  
  
     您可以使用管理中心判斷識別。 在 [安全性] 區段中開啟 [設定服務帳戶]****，以檢視哪一個 Windows 帳戶與每一個應用程式所使用的服務應用程式集區相關聯，然後依照本主題所提供的指示將管理權限授與帳戶。  
  
##  <a name="grant-read-permissions-on-the-tabular-model-database"></a><a name="bkmk_BISM"></a> 授與表格式模型資料庫的讀取權限  
 由於資料庫在伺服器陣列外部的伺服器上執行，因此在設定連接的過程中，將會包含授與後端 Analysis Services 伺服器的資料庫使用者權限。 Analysis Services 會使用以角色為基礎的權限模型。 連接到模型資料庫的使用者必須使用「讀取」權限或更高的權限，透過授與讀取權限給其成員的角色來進行。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立模型時會定義角色 (有時也會定義角色成員資格)。 您不能使用 SQL Server Management Studio 建立角色，但是可以用來將成員加入至已經定義的角色。 如需建立角色的詳細資訊，請參閱[建立及管理角色 &#40;SSAS 表格式&#41;](../tabular-models/roles-ssas-tabular.md)。  
  
#### <a name="assign-role-membership"></a>指派角色成員資格  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，然後在 [物件總管] 中展開資料庫，再展開 [角色]****。 您應該看到已定義的角色。 如果角色不存在，請與模型的作者聯繫，並要求加入角色。 在 Management Studio 中看到角色之前，必須重新部署模型。  
  
2.  以滑鼠右鍵按一下角色，然後選取 [**屬性**]。  
  
3.  在 [成員資格] 頁面中，加入需要存取權的 Windows 群組和使用者帳戶。  
  
##  <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a><a name="bkmk_connect"></a> 建立與表格式模型資料庫的 BI 語意模型連接  
 在 Analysis Services 中設定權限之後，您可以返回 SharePoint 並建立 BI 語意模型連接。  
  
1.  在包含 BI 語意模型連接的文件庫中，按一下 SharePoint 功能區上的 [文件]****。  
  
2.  按一下 [新文件] 上的向下箭號，然後選取 [BI 語意模型連接檔案]****，開啟 [新增 BI 語意模型連接] 頁面。  
  
3.  同時設定 [伺服器]**** 和 [資料庫]**** 屬性。 如果您不確定資料庫名稱，請使用 SQL Server Management Studio 檢視在伺服器上部署之資料庫的清單。  
  
     [伺服器名稱]**** 可以是伺服器的網路名稱、IP 位址或完整網域名稱 (例如 myserver.mydomain.corp.adventure-works.com)。 如果伺服器當做具名執行個體安裝，請使用下列格式輸入伺服器名稱：computername\instancename。  
  
     [資料庫]**** 必須是目前可以在伺服器上使用的表格式資料庫。 請勿指定另一個 BI 語意模型連接檔案、Office 資料連線 (.odc) 檔案、Analysis Services OLAP 資料庫或 PowerPivot 活頁簿。 若要取得資料庫名稱，您可以使用 Management Studio 連接到伺服器並檢視可用資料庫的清單。 使用資料庫的屬性頁可確保您擁有正確的名稱。  
  
4.  按一下 [確定]**** 以儲存頁面。 此時，PowerPivot 服務應用程式會驗證該連接。  
  
     如果連接資訊是正確的，而且您已經將管理權限授與 PowerPivot 服務應用程式，讓它以目前使用者的身分連接到 Analysis Services，驗證就會成功。  
  
     如果連接資訊是錯誤的，或服務應用程式缺少權限，驗證就會失敗。 頁面上會顯示驗證訊息，詢問您是否要儲存檔案。 如果您知道連接是有效的，還是應該儲存檔案，因為錯誤是缺少權限所致，而不是連接資訊無效。  
  
     您可以在 Excel 或 Power View 中使用它來連接到表格式模型資料庫，藉以驗證連接。 如果資料來源連接成功，儘管驗證警告，連接仍然有效。  
  
##  <a name="configure-sharepoint-permissions-on-the-bi-semantic-model-connection"></a><a name="bkmk_permissions"></a>設定 BI 語義模型連接的 SharePoint 許可權  
 需要有 SharePoint 文件庫中 BI 語意模型連接項目的 [讀取]**** 權限，才能使用 BI 語意模型連接作為 Excel 活頁簿或 Reporting Services 報表的資料來源。 [讀取] 權限等級包含 [開啟項目]**** 權限，此權限允許將 BI 語意模型連接資訊下載到 Excel 桌面應用程式。  
  
 有數種方法可以在 SharePoint 中授與權限。 下列指示說明如何建立具有 [讀取]**** 權限等級、稱為「BISM 使用者」**** 的新群組。  
  
 您必須是網站擁有者，才能變更權限。  
  
1.  在 [網站動作] 中，按一下 [網站權限]****。  
  
2.  按一下 [建立群組]****，並將新群組命名為「BISM 使用者」****。  
  
3.  選擇 [讀取]**** 權限等級，然後按一下 [建立]****。  
  
4.  選取 [人員與群組] 中的 [BISM 使用者]****。  
  
5.  指向 [新增]，按一下 [加入使用者]****，然後加入使用者或群組帳戶。  
  
     這些使用者和群組現在具有整個網站 (包括從網站層級繼承權限的所有文件庫和清單) 的讀取權限。 如果這些權限太高，您可以從特定文件庫、清單或項目中選擇地移除此群組。  
  
 若要選擇地在項目層級移除權限，請執行下列動作：  
  
1.  在文件庫中，選取文件。 按一下右下箭頭，然後按一下 [管理權限]****。  
  
2.  根據預設，項目會繼承權限。 若要變更此文件庫中個別文件的權限，請按一下 [停止繼承權限]****。  
  
3.  選取 [BISM 使用者]**** 旁邊的核取方塊。  
  
4.  按一下 [移除使用者權限]****。  
  
##  <a name="next-steps"></a><a name="bkmk_next"></a> 後續步驟  
 在建立 BI 語意模型連接並且確保其安全之後，可以將此連接指定為資料來源。 如需詳細資訊，請參閱 [在 Excel 或 Reporting Services 使用 BI 語意模型連接](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot BI 語義模型連接 &#40;. bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [建立與 PowerPivot 活頁簿的 BI 語意模型連接](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  
