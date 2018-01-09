---
title: "建立資料來源 (SSAS 多維度) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.impersonationinfo.f1
- sql13.asvs.connectionmanager.f1
- sql13.asvs.datasourcedesigner.f1
helpviewer_keywords:
- impersonation [Analysis Services]
- data sources [Analysis Services], creating
- security [Analysis Services], data source connections
ms.assetid: 9fab8298-10dc-45a9-9a91-0c8e6d947468
caps.latest.revision: "61"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 213bc7a17344f42cd10258962f91711a5ee3acba
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-data-source-ssas-multidimensional"></a>建立資料來源 (SSAS 多維度)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]多維度模型中，資料來源物件代表您所處理 （或匯入） 的資料來源的連接資料。 多維度模型至少必須包含一個資料來源物件，不過您可以加入更多資料來源物件，以便結合數個資料倉儲的資料。 使用本主題中的說明為您的模型建立資料來源物件。 如需設定這個物件之屬性的詳細資訊，請參閱[設定資料來源屬性 &#40;SSAS 多維度&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)。  
  
 本主題包含下列各節：  
  
 [選擇資料提供者](#bkmk_provider)  
  
 [設定認證和模擬選項](#bkmk_impersonation)  
  
 [檢視或編輯連接屬性](#bkmk_ConnectionString)  
  
 [使用資料來源精靈建立資料來源](#bkmk_steps)  
  
 [使用現有的連接建立資料來源](#bkmk_connection)  
  
 [在模型中加入多個資料來源](#bkmk_multipleDS)  
  
##  <a name="bkmk_provider"></a> 選擇資料提供者  
 您可以使用 Managed [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 或原生 OLE DB 提供者進行連接。 建議之 SQL Server 資料來源的資料提供者是 SQL Server Native Client，因為其通常提供較佳的效能。  
  
 若為 Oracle 及其他協力廠商資料來源，請檢查協力廠商是否提供原生 OLE DB 提供者，並先嘗試此原生 OLE DB 提供者。 如果發生錯誤，請嘗試 [連接管理員] 中列出的其他 .NET 提供者或原生 OLE DB 提供者。 確定您使用的任何資料提供者，已安裝在用來開發及執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 方案的所有電腦上。  
  
##  <a name="bkmk_impersonation"></a> 設定認證和模擬選項  
 資料來源連接有時可以使用 Windows 驗證或資料庫管理系統提供的驗證服務，例如連接至 SQL Azure 資料庫時使用 SQL Server 驗證。 您指定的帳戶必須擁有遠端資料庫伺服器的登入及外部資料庫的讀取權限。  
  
### <a name="windows-authentication"></a>Windows 驗證  
 使用 Windows 驗證的連接會在資料來源設計師的 [模擬資訊] 索引標籤中指定。 使用這個索引標籤即可選擇模擬選項，以指定連接至外部資料來源時，執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的帳戶。 並非所有選項都可以在所有案例中使用。 如需這些選項及何時使用這些選項的詳細資訊，請參閱[設定模擬選項 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)。  
  
### <a name="database-authentication"></a>資料庫驗證  
 若不使用 Windows 驗證，您也可以指定連接使用資料庫管理系統所提供的驗證服務。 在某些情況下，需要使用資料庫驗證。 需要使用資料庫驗證的情況包括：使用 SQL Server 驗證連接至 Windows Azure SQL 資料庫，或存取在不同作業系統或非信任網域中執行的關聯式資料來源。  
  
 對於使用資料庫驗證的資料來源，會在連接字串中指定資料庫登入的使用者名稱和密碼。 若在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 模型中設定資料來源連接，當您於 [連接管理員] 中輸入使用者名稱和密碼時，即會將認證新增至連接字串。 記得指定具有資料讀取權限的使用者識別。  
  
 擷取資料時，建立連接的用戶端程式庫會構成在連接字串中包含認證的連接要求。 [模擬資訊] 索引標籤中的 Windows 驗證認證選項不會用於連接，但可用於其他作業，例如存取本機電腦上的資源。 如需詳細資訊，請參閱[設定模擬選項 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)。  
  
 在模型中儲存資料來源物件之後，即會加密連接字串和密碼。  基於安全性的理由，當您後續在工具、指令碼或程式碼中檢視時，會隱藏連接字串中的密碼。  
  
> [!NOTE]  
>  依預設， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 不會在連接字串中儲存密碼。 如果未儲存此密碼， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在需要時提示您輸入密碼。 如果您選擇儲存密碼，此密碼會以加密格式儲存在資料連接字串中。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用包含資料來源之資料庫的資料庫加密金鑰來加密資料來源的密碼資訊。 將連接資訊加密之後，您必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來變更 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務帳戶或密碼，否則將無法復原加密的資訊。 如需詳細資訊，請參閱 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)。  
  
### <a name="defining-impersonation-information-for-data-mining-objects"></a>定義資料採礦物件的模擬資訊  
 資料採礦查詢可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務帳戶的內容中執行，但是也可以在使用者提交查詢的內容或指定之使用者的內容中執行； 查詢執行所在的內容可能會影響查詢結果。 如果是資料採礦 **OPENQUERY** 類型的作業，您可能會希望資料採礦查詢在目前使用者的內容或指定之使用者的內容中執行 (不論執行查詢的使用者是誰)，而不是在此服務帳戶的內容中執行。 如此可使用有限的安全性認證來執行查詢。 如果您希望 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 模擬目前的使用者或是模擬指定的使用者，請選取 [使用特定的使用者名稱和密碼] 或 [使用目前使用者的認證] 選項。  
  
##  <a name="bkmk_steps"></a> 使用資料來源精靈建立資料來源  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟您想要在其中定義資料來源的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，或是連接到您想要在其中定義資料來源的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
2.  在**方案總管**中，以滑鼠右鍵按一下 [資料來源] 資料夾，然後按一下 [新增資料來源] 啟動 [資料來源精靈]。  
  
3.  在 [選取如何定義連接] 頁面上，選擇 [依據現有的或新的連接建立資料來源]，然後按一下 [新增] 開啟 [連線管理員]。  
  
     新的連接是在連接管理員中建立。 在連接管理員中選取提供者，然後指定該提供者用來連接基礎資料的連接字串屬性。 所需的確切資訊需視所選的提供者而定，但是這類資訊通常包括伺服器或服務執行個體、用來登入此伺服器或服務執行個體的資訊、資料庫或檔案名稱，以及其他提供者特有的設定。 此程序的其餘部分將假設存在 SQL Server 資料庫連接。  
  
4.  選取連接所用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 或原生 OLE DB 提供者。  
  
     新連接的預設提供者為原生 OLE DB\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者。 此提供者是用來連接到使用 OLE DB 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 執行個體。 若要連接到 SQL Server 關聯式資料庫，使用原生 OLE DB\SQL Server Native Client 11.0 通常會比使用其他提供者更快。  
  
     您可以選擇不同的提供者來存取其他資料來源。 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支援的提供者和關聯式資料庫清單，請參閱 [支援的資料來源 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)。  
  
5.  輸入選定提供者所要求的資訊，以連接到基礎資料來源。 如果已選取**原生 OLE DB\SQL Server Native Client**提供者，請輸入下列資訊：  
  
    1.  [伺服器名稱] 是 Database Engine 執行個體的網路名稱。 您可以將它指定為 IP 位址、電腦的 NETBIOS 名稱或完整網域名稱。 如果伺服器安裝成具名執行個體，您必須包含執行個體名稱 (例如，\<電腦名稱 >\\< instancename\>)。  
  
    2.  [登入伺服器] 會指定驗證連接的方式。 [使用 Windows 驗證] 會使用 Windows 驗證。 [使用 SQL Server 驗證] 會針對支援混合模式驗證的 Windows Azure SQL Database 或 SQL Server 執行個體指定資料庫使用者登入。  
  
        > [!IMPORTANT]  
        >  [連線管理員] 會針對使用 SQL Server 驗證的連接加入 [儲存我的密碼] 核取方塊。 雖然系統一定會顯示此核取方塊，但是不一定會使用它。  
        >   
        >  Analysis Services 不使用此核取方塊的狀況包括重新整理或處理作用中 Analysis Services 資料庫所使用的 SQL Server 關聯式資料。 不論您清除或選取 [儲存我的密碼]，Analysis Services 一定會加密並儲存密碼。 密碼將經過加密並且同時儲存在 .abf 和資料檔案中。 這種行為存在的原因是，Analysis Services 不支援在伺服器上儲存工作階段架構的密碼。  
        >   
        >  這種行為僅適用於 a) 保存在 Analysis Services 伺服器執行個體上的資料庫，以及 b) 使用 SQL Server 驗證來重新整理或處理關聯式資料的資料庫。 它不適用於您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中設定而且僅用於工作階段持續時間的資料來源連接。 雖然您無法移除已經儲存的密碼，不過可以使用不同的認證或 Windows 驗證來覆寫目前與資料庫一起儲存的使用者資訊。  
  
    3.  [選取或輸入資料庫名稱] 或 [附加資料庫檔案] 是用來指定資料庫。  
  
    4.  在此對話方塊的左側按一下 [全部]，即可檢視這個連接的其他設定，包括這個提供者的所有預設值。  
  
    5.  依適當情況變更環境的設定，然後按一下 [確定]。  
  
         新的連接即會出現在「資料來源精靈」之 [選取如何定義連接] 頁面的 [資料連接] 窗格中。  
  
6.  按 [下一步] 。  
  
7.  在 [模擬資訊] 中，指定 Analysis Services 連接外部資料來源時使用的 Windows 認證或使用者識別。 如果您針對連接使用資料庫驗證，則會忽略這些設定。  
  
     根據您使用資料來源的方式而定，選擇模擬選項的指導方針會有所不同。 如果是處理工作，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務在連接到資料來源時，必須在其服務帳戶或指定之使用者帳戶的安全性內容中執行。  
  
    -   [使用特定的 Windows 使用者名稱和密碼] 會指定一組唯一的最低權限認證。  
  
    -   [使用服務帳戶] 會使用服務識別處理資料。  
  
     您指定的帳戶必須擁有資料來源的讀取權限。  
  
8.  按 [下一步] 。  在 [正在完成精靈] 中，輸入資料來源名稱或使用預設名稱。 預設名稱是連接中所指定資料庫的名稱。 [預覽] 窗格會顯示這個新資料來源的連接字串。  
  
9. 按一下 **[完成]**。  方案總管中的 [資料來源] 資料夾會顯示新的資料來源。  
  
##  <a name="bkmk_connection"></a> 使用現有的連接建立資料來源  
 當您在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中工作時，您的資料來源可以根據方案中的現有資料來源，也可以根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 [資料來源精靈] 提供幾個選項用於建立資料來源物件，包括使用相同專案中的現有連接。  
  
-   根據方案中的現有資料來源來建立資料來源時，可讓您定義與現有資料來源同步的資料來源。 當建立包含這個新資料來源的專案時，會使用基礎資料來源中的資料來源設定。  
  
-   根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案建立資料來源時，可讓您參考目前專案中方案內的另一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 新的資料來源會搭配其 [資料來源] 屬性和 [初始目錄] 屬性 (從選定專案的 **TargetServer** 和 **TargetDatabase** 屬性取得) 使用 MSOLAP 提供者。 在使用多個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案來管理遠端資料分割的方案中，此功能很有用，因為來源和目的地 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫都需要對應的資料來源來支援遠端資料分割的儲存和處理。  
  
 當您參考資料來源物件時，只能在參考的物件或專案中編輯該物件， 您無法在包含此參考的資料來源物件中編輯連接字串。 參考的物件或專案中的連接資訊變更會在建立新的資料來源時，出現在其中。 當您建立專案或清除資料來源設計師中的參考時，會同步處理出現在專案之資料來源 (.ds) 檔案中的連接字串資訊。  
  
##  <a name="bkmk_ConnectionString"></a> 檢視或編輯連接屬性  
 連接字串是根據您在 [資料來源設計師] 或 [新增資料來源精靈] 中選取的屬性所構成。 您可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中檢視連接字串及其他屬性。  
  
 **若要編輯連接字串**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的方案總管中，按兩下資料來源物件。  
  
2.  按一下 [編輯]，然後按一下左瀏覽窗格中的 [全部]。  
  
3.  屬性方格隨即出現，顯示您所使用資料提供者的可用屬性。 如需有關這些屬性的詳細資訊，請參閱提供者的產品文件集。  若是 SQL Server Native Client，請參閱 [搭配 SQL Server Native Client 使用連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 若您在方案中有多個資料來源物件，但只想在一處維護連接字串，則可將目前資料來源設定為參考其他資料來源物件。  
  
 「資料來源參考」是與另一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或相同方案中的資料來源之關聯。 參考會提供方法來同步處理方案中物件之間的資料來源。 連接字串資訊在您建立專案時都會同步處理。 若要變更參考另一個物件之資料來源的連接字串，您必須變更參考之物件的連接字串。  
  
 您可清除核取方塊來移除參考。 這樣即可結束物件間的同步處理，並讓您可以變更資料來源中的連接字串。  
  
##  <a name="bkmk_multipleDS"></a> 在模型中加入多個資料來源  
 您可以建立多個資料來源物件，以支援與其他資料來源的連接。 每個資料來源都必須擁有可用來建立關聯性的資料行。  
  
> [!NOTE]  
>  如果已定義多個資料來源，而且在單一查詢中查詢多個來源的資料 (例如針對雪花維度)，您必須使用 **OpenRowset**定義支援遠端查詢的資料來源。 一般來說，這會是 Microsoft SQL Server 資料來源。  
  
 使用多個資料來源的需求如下：  
  
-   指定一個資料來源做為主要資料來源。 主要資料來源會用來建立資料來源檢視。  
  
-   主要資料來源必須支援 **OpenRowset** 函數。  如需 SQL Server 中這個函數的詳細資訊，請參閱 <xref:Microsoft.SqlServer.TransactSql.ScriptDom.TSqlTokenType.OpenRowSet>。  
  
 使用下列方法結合來自多個資料來源的資料：  
  
1.  在模型中建立資料來源。  
  
2.  使用 SQL Server 關聯式資料庫做為資料來源，建立資料來源檢視。 這是您的主要資料來源。  
  
3.  在資料來源檢視設計師中，使用您剛才建立的資料來源檢視，以滑鼠右鍵按一下工作區中的任意位置，然後選取 [加入/移除資料表]。  
  
4.  選擇第二個資料來源，然後選取您要加入的資料表。  
  
5.  尋找並選取您加入的資料表。 以滑鼠右鍵按一下資料表，然後選取 [新增關聯性]。 選擇包含相符資料的來源和目的地資料行。  
  
## <a name="see-also"></a>請參閱  
 [支援的資料來源 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
