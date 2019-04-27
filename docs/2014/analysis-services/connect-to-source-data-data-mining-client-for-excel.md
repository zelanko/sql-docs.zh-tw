---
title: 連線至資料來源 （適用於 Excel 的資料採礦用戶端） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
ms.assetid: 548672ce-e403-4aca-b67a-c2c797f053dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78c60832ea6111b0682e8a6d2b5ab3540a19cfb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680250"
---
# <a name="connect-to-source-data-data-mining-client-for-excel"></a>連接到來源資料 (適用於 Excel 的資料採礦用戶端)
  本主題將說明如何建立和使用用於儲存資料採礦模型的連接，以及用於存取 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中儲存之外部資料的連接。  
  
 **資料採礦連接。** 在您啟動增益集時建立的初始連接是用於存取演算法、分析資料，以及儲存採礦結構和模型。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接是在增益集中使用模型和視覺效果工具的必要條件，因為這些增益集相依於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 所提供的演算法和資料結構。  
  
 **外部資料來源的連接。** 您也可以在建立模型或儲存結果時建立外部資料的連接。 例如，您可以在某個伺服器上建立資料採礦模型，然後使用另一個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體、Excel 資料表或 [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 之類的外部資料來源中儲存之資料，對資料採礦模型執行預測查詢。 每次您存取新的資料來源時，系統都會提示您使用對話方塊來建立連接。  
  
##  <a name="bkmk_prereq2"></a> 必要條件  
 此版本的增益集需要 SQL Server 2012 的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。 如果您要連接到舊版的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，則可以使用增益集的另一個版本。 目前有其他支援 SQL Server 2005、SQL Server 2008 和 SQL Server 2008 R2 的增益集版本。  
  
 若要連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，您必須擁有存取資料庫伺服器的權限。 而且，資料採礦工作階段必須已啟用，您也必須有伺服器上儲存之資料庫物件的讀取或讀取/寫入權限。  
  
##  <a name="bkmk_connect"></a> 建立資料採礦伺服器連接  
 **連線**for Excel 會提供工具來管理執行個體的連接，資料採礦用戶端群組 Excel 的資料表分析工具[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
-   您可以在安裝增益集時建立連接，或稍後新增連接。  
  
-   除非您正在進行建立或查詢模型的程序，否則可以建立多個連接，並且隨時變更連接。  
  
     在處理資料採礦模型時，不要變更或關閉連接。 資料採礦模型可能會遺失資料，或模型可能會變成無法使用。  
  
-   一次只能有一個作用中的連接。  
  
### <a name="connections-in-the-excel-add-ins"></a>Excel 增益集的連接  
 **連線**for Excel 是您用來管理的執行個體的連線，資料採礦用戶端群組 Excel 的資料表分析工具[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
##### <a name="create-a-new-server-connection-in-the-excel-add-ins"></a>在 Excel 增益集中建立新的伺服器連接  
  
1.  按一下 **連接**按鈕**分析**或是**Data Mining**功能區。  
  
    > [!NOTE]  
    >  按鈕的文字表示連接是否存在。 當工作表中不建立任何連線時，按鈕會包含文字"\<沒有連接 >。 」 如果先前已在活頁簿中建立連接，該連接名稱會出現在按鈕上。  
  
2.  在 [ **Analysis Services 連接**] 對話方塊中，按一下**新增**。  
  
3.  在 **新的 Analysis Services 連接**對話方塊方塊中，輸入伺服器的名稱。  
  
4.  指定驗證方法。  
  
5.  選取 將資料庫從**目錄名稱**下拉式清單。 如果資料庫不存在的執行個體上，選取 **（預設值）**。  
  
6.  輸入連接的易記名稱。  
  
7.  按一下 **測試連接**來確認伺服器和資料庫可供使用。  
  
8.  按一下 **[確定]**，然後按一下 **[關閉]**。  
  
### <a name="connections-using-a-web-service"></a>使用 Web 服務的連接  
 如果您要使用精簡型用戶端架構來啟用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cube 和資料的瀏覽，也可以透過 Web 服務設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器的連接。 如需有關如何定義網路架構用戶端的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》。  
  
 如果您可以存取已針對 Web 服務設定的伺服器，當您初次建立連接時可以指定連接類型。  
  
##### <a name="create-an-http-connection-to-analysis-services"></a>建立 Analysis Services 的 HTTP 連接  
  
1.  開啟**新的 Analysis Services 連接** 對話方塊。  
  
2.  對於伺服器名稱，請輸入 http://，後面接著指派給 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器的 URL。  
  
3.  輸入存取 Web 服務所需的使用者名稱和密碼。  
  
### <a name="connections-in-the-visio-add-in"></a>Visio 增益集的連接  
 不同於 Excel，Visio 沒有提供工具功能區，而且沒有特別用於建立或監視連接的按鈕。 但在您初次選取資料採礦圖形並將它放入 Visio 頁面時，就會建立資料連接。 精靈會提示您選取圖形的模型以及設定其他選項。  
  
 如果您先前已在 Excel 中使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源的連接，這些連接會列為可從中選取的可能資料來源。  
  
##### <a name="create-a-connection-for-a-visio-shape"></a>建立 Visio 圖形的連接  
  
1.  開啟資料採礦範本，然後選取其中一個資料採礦圖形。  
  
2.  將圖形拖放至空白頁面上。  
  
3.  在  **Zdroj dat**對話方塊中，選取資料來源從清單中，或按一下**新增**。  
  
4.  如果您選取**新增**，請依照下列程序稍早所述來指定伺服器和目錄名稱，或透過 Web 服務連線。  
  
##  <a name="bkmk_change"></a> 變更連接  
 您可以在相同工作表中建立多個連接，但每次只能有一個作用中的連接。 目前連接的名稱會顯示在**連線** 按鈕。  
  
 適用於 Excel 的資料採礦用戶端，您也可以驗證的連接字串和目前連接的狀態，即可**追蹤**，然後按一下**目前連接**。  
  
#### <a name="use-a-different-server-connection"></a>使用不同的伺服器連接  
  
1.  按一下 **連線**。  
  
2.  在 [ **Analysis Services 連接**] 窗格中選取連接從**其他連接**清單，然後按**設為現用**。  
  
3.  按一下 **測試連接**來驗證連線是否可用。  
  
 在採礦模型完成處理之後，會在本機儲存結果，如果您關閉與某個伺服器的連接，然後連接到另一個伺服器，這對資料沒有影響。 不過，您應避免在處理資料採礦模型時變更連接或中斷連接，因為這可能會損毀資料。  
  
#### <a name="modify-an-existing-server-connection"></a>修改現有的伺服器連接  
  
1.  您無法修改現有的連接。如果您想要連接到不同的資料庫或不同的伺服器，就應該建立新的連接。  
  
2.  如果您必須修改連接字串以增加查詢逾時或加入 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體特有的其他參數，其中一個選項就是編輯儲存連接字串的 .dmc 檔案。  
  
     \<磁碟機： > \Users\\< myusername\>\AppData\Local\Microsoft\Data 採礦增益集  
  
##  <a name="bkmk_extconnections"></a> 連接到外部資料來源  
 而在工具**分析**功能區專門處理 Excel 中的工具中的資料**Data Mining**功能區可讓您直接連接到外部資料來源當做輸入，針對您的模型，或取樣。  
  
 這些增益集中的下列工具支援使用外部資料進行資料採礦：  
  
-   [範例資料&#40;SQL Server 資料採礦增益集&#41;](sample-data-sql-server-data-mining-add-ins.md)  
  
-   [分類精靈&#40;資料採礦適用於 Excel 的增益集&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
-   [估計精靈&#40;資料採礦適用於 Excel 的增益集&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
-   [叢集精靈&#40;資料採礦適用於 Excel 的增益集&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
-   [預測精靈&#40;資料採礦適用於 Excel 的增益集&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
-   [建立採礦結構&#40;SQL Server 資料採礦增益集&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
-   [精確度圖表&#40;SQL Server 資料採礦增益集&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
-   [收益圖&#40;SQL Server 資料採礦增益集&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
  
-   [分類矩陣&#40;SQL Server 資料採礦增益集&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
### <a name="using-analysis-services-as-a-data-source"></a>使用 Analysis Services 做為資料來源  
 您無法直接存取儲存在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cube 或表格式模型中的資料。 請改在 Excel 中建立 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器的連接，然後使用資料來建立模型。  
  
### <a name="relational-data-sources"></a>關聯式資料來源  
 如果您想要使用關聯式來源中的資料做為模型的輸入，可以連接到下列 SQL Server 版本：  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
 您也可以從 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援當做資料來源使用的任何其他關聯式資料來源取得資料。 如需支援的資料來源的資訊，請參閱[多維度模型中的資料來源](multidimensional-models/data-sources-in-multidimensional-models.md)  
  
 請注意，下列資料類型無法用於資料採礦，而且如果您在建立模型時加入這些資料類型，將會產生錯誤：  
  
-   ntext  
  
-   BINARY  
  
## <a name="see-also"></a>另請參閱  
 [追蹤&#40;適用於 Excel 的資料採礦用戶端&#41;](trace-data-mining-client-for-excel.md)  
  
  
