---
title: "建立報表資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bd6662c7-ffbe-479d-8944-3dc858340998
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b941dc8eb4fb1f0fc14d2565c8f1f65dd3ba4d15
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-report-data-source"></a>建立報表資料來源
  為了讓 Power View 連接到多維度模型，您必須在 SharePoint 文件庫中建立共用報表資料來源定義，也稱為 .rsds 檔。 .rsds 檔會指定 Analysis Services 伺服器執行個體的名稱、連接類型、連接字串，以及用來連接到多維度模型的認證。 當使用者按下 .rsds 時，新的空白 Power View 報表 (.rdlx 檔) 就會在瀏覽器中開啟。  
  
 若要建立 .rsds 連接，您必須已安裝 SQL Server 2012 (或更新版本) Reporting Services 以及適用於 SharePoint 2010 或 SharePoint 2013 的 Reporting Services 增益集。  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>建立多維度模型的報表資料來源 (.rsds) 連接  
 在開始進行之前，您需要先了解：  
  
-   以多維度模式執行之 Analysis Services 伺服器執行個體的名稱。  
  
-   要連接的多維度資料庫名稱。  
  
-   Cube 的名稱 (如果有多個的話)。  
  
-   (選擇性) 檢視方塊名稱。  
  
-   (選擇性) 地區設定識別碼。  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>若要建立共用報表資料來源 (.rsds) 檔案 (SharePoint 2010)  
  
1.  按一下文件庫功能區上的 [文件] 索引標籤。  
  
2.  按一下 [新增文件] > [報表資料來源]。  
  
    > [!NOTE]  
    >  如果您沒有在功能表上看見 [報表資料來源] 項目，表示此文件庫的報表資料來源內容類型尚未啟用。 如需詳細資訊，請參閱[將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
3.  在 [資料來源屬性] 頁面的 [名稱] 中，輸入連接 .rsds 檔案的名稱。  
  
4.  在 [資料來源類型] 中，選取 [Power View 的 Microsoft 商業智慧語意模型]。  
  
5.  在 [連接字串] 中，指定 Analysis Services 伺服器名稱、資料庫名稱、Cube 名稱及任何選擇性設定。  
  
     連接字串： `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>’`  
  
    > [!NOTE]  
    >  如果有多個 Cube，則必須指定 Cube 名稱。  
  
     (選擇性) Cube 可以包含檢視方塊，為使用者提供在用戶端中只看到某些維度和/或量值群組的精選檢視。 若要指定檢視方塊，請輸入檢視方塊名稱做為 Cube 屬性的值： `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>’`  
  
     (選擇性) 在模型中，可以指定各種語言的 Cube 中繼資料和資料翻譯。 若要顯示翻譯 (資料和中繼資料)，您必須將 "Locale Identifier" 屬性加入連接字串： `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>’; Locale Identifier=<identifier number>`  
  
6.  在 [認證] 中，指定報表伺服器取得認證來存取外部資料來源的方式。  
  
    -   如果您想要使用開啟報表之使用者的認證來存取資料，請選取 [Windows 驗證 (整合式)]。 如果 SharePoint 網站或伺服陣列使用表單驗證或透過受信任帳戶連接到報表伺服器，請勿選取這個選項。 如果您想要排程這個報表的訂閱或資料處理，請勿選取這個選項。 在針對網域啟用 Kerberos 驗證時，或者資料來源與報表伺服器是在同一部電腦上時，此選項具有最佳的效能。 如果未啟用 Kerberos 驗證，Windows 認證只能傳遞至一部其他電腦。 這表示，如果外部資料來源位於另一部需要其他連接的電腦上，您就會收到錯誤而非所預期的資料。  
  
    -   選取**提示認證**他或她如果您想讓使用者輸入其認證每次執行報表。 如果您想要排程這個報表的訂閱或資料處理，請勿選取這個選項。  
  
    -   選取**預存認證**如果您想要使用一組認證存取資料。 認證會先經過加密，然後再儲存。 您可以選取決定預存認證之驗證方式的選項。 如果預存認證屬於 Windows 使用者帳戶，請選取 [當做 Windows 認證使用]。 如果您想在資料庫伺服器上設定執行內容，請選取 [設定執行內容到這個帳戶]。  
  
    -   如果您在連接字串中指定認證，或是想要使用最低權限帳戶來執行報表，請選取 [不需要認證]。  
  
7.  按一下 [測試連接] 進行驗證。  
  
8.  如果您想要讓資料來源成為使用中，請選取 [啟用此資料來源]。 如果資料來源已設定，但是非使用中，當使用者嘗試建立報表時，就會收到錯誤訊息。  
  
  

