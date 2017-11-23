---
title: "用於 Analysis Services 連接的資料提供者 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 51b41114385321e84511c188077e48455d1678a2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="data-providers-used-for-analysis-services-connections"></a>用於 Analysis Services 連接的資料提供者
  Analysis Services 會為伺服器和資料存取提供三個資料提供者。 所有連接到 Analysis Services 的應用程式都會使用其中一個提供者來進行存取。 其中兩個提供者 ADOMD.NET 和 Analysis Services 管理物件 (AMO) 為 Managed 資料提供者。 Analysis Services OLE DB 提供者 (MSOLAP DLL) 是原生資料提供者。  
  
 如果組織執行多個 Analysis Services 版本，您可能需要在連接至 Analysis Services 資料的使用者工作站上安裝較新版本的資料提供者。 若要連接至較新版本的 Analysis Services，您必須使用同一個主要版本的資料提供者。 例如，若要連接至 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]，每一個工作站都必須有相同版本的資料提供者。 儘管 Excel 會安裝其進行連接所需的資料提供者，但是該提供者可能比您所使用的 Analysis Services 執行個體還要舊。  
  
 本主題包含下列幾節：  
  
 [如何判斷伺服器版本](#bkmk_ServVers)  
  
 [如何判斷 Analysis Services 資料提供者版本](#bkmk_LibUpdate)  
  
 [何處可取得較新版的資料提供者](#bkmk_downloadsite)  
  
 [Analysis Services OLE DB 提供者](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="bkmk_ServVers"></a> 如何判斷伺服器版本  
 若得知 Analysis Services 執行個體的版本，將有助於您判斷是否需要在組織中的工作站上安裝較新版的資料提供者。  
  
-   在 SQL Server Management Studio 中，連接到 Analysis Services 執行個體。 您可以在 [伺服器屬性] > [一般] > [版本] 中檢視版本資訊。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 最初發行版本的主要組建編號為 13.0.1601.5。  
  
  
##  <a name="bkmk_LibUpdate"></a> 如何判斷 Analysis Services 資料提供者版本  
 資料提供者會隨 Analysis Services 一起安裝，而例行性連接到 Analysis Services 資料庫的用戶端應用程式 (例如 Excel) 也會加以安裝。  
  
 Office 2010 會從 SQL Server 2008 安裝資料提供者。 Office 2013 會從 SQL Server 2012 等安裝資料提供者。 如果您使用多個版本的 Office 或 SQL Server，然而連接或功能可用性不如預期，您可能需要安裝較新版的資料提供者。 您可以在同一部電腦上同時執行各資料提供者的多個主要版本。  
  
#### <a name="find-the-file-version-of-the-oledb-provider"></a>查出 OLEDB 提供者的檔案版本  
  
1.  移至 \Program Files\Microsoft Analysis Services\AS OLEDB\130。  
  
2.  以滑鼠右鍵按一下 [msolap130.dll] > [屬性] > [詳細資料]。  
  
 如果您在此位置找不到該檔案，或是資料夾路徑包含 AS OLEDB\110 或 AS OLEDB\90，表示您目前使用的是舊版程式庫，必須安裝較新版本 (AS OLEDB\11) 才能連接至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
#### <a name="find-the-file-version-of-adomdnet-and-amo"></a>查出 ADOMD.NET 和 AMO 的檔案版本  
  
1.  移至 C:\Windows\Assembly。  
  
2.  以滑鼠右鍵按一下 Microsoft.AnalysisServices.AdomdClient，再按一下 [內容]。 按一下 **[版本]**。  
  
     針對 AMO，以滑鼠右鍵按一下 Microsoft.AnalysisServices。  
  
##  <a name="bkmk_downloadsite"></a> 何處可取得較新版的資料提供者  
 用戶端電腦上安裝的版本應與提供資料的伺服器主要版本相符。 如果伺服器安裝比網路中工作站上安裝的資料提供者還要新，您可能需要安裝較新版的程式庫。  
  
#### <a name="find-the-data-providers-on-the-download-site"></a>從下載網站找到資料提供者  
  
1.  移至 [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52676)。  
  
2.  按一下 [下載]。 ADOMD.NET、 OLE DB 提供者和 AMO 清單中包含以可安裝的套件。 例如，SQL_AS_OLEDB.msi。 每一套程式庫都有 32 位元或 64 位元版本可選。 執行 64 位元作業系統的伺服器和新型工作站需要 64 位元版本。  
  
##  <a name="bkmk_OLE"></a> Analysis Services OLE DB 提供者  
 Analysis Services OLE DB 提供者是 Analysis Services 資料庫連接的原生提供者。 MSOLAP 是間接供 ADOMD.NET 和 AMO 使用，而將連接要求委派給資料提供者。 如果方案需求致使您無法使用 Managed API，您也可以直接從應用程式的程式碼呼叫 OLE DB 提供者。  
  
 Analysis Services OLE DB 提供者是由 SQL Server 安裝程式、Excel 以及其他經常用來存取 Analysis Services 資料庫的應用程式所自動安裝的。 您也可從下載中心下載此元件再以手動方式安裝。 根據預設，您可以在 \Program Files\Microsoft Analysis Services 資料夾中找到此提供者。 您必須在所有用來存取 Analysis Services 資料的工作站上安裝此提供者。  
  
 MSOLAP130.dll 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]隨附的 Analysis Services OLE DB 提供者版本。 其他最近的上一個版本包括 MSOLAP110.dll (適用於 SQL Server 2008 及 2008 R2) 及 MSOLAP90.dll (適用於 SQL Server 2005)。  
  
 OLE DB 提供者通常會在連接字串中指定。 Analysis Services 連接字串使用不同的命名法來參考的 OLE DB 提供者： MSOLAP。\<版本 >.dll  
  
 MSOLAP.5.dll 是目前和 Excel 2013 搭配安裝的 Analysis Services OLE DB 提供者。 較舊的版本如 MSOLAP.4.dll 或 MSOLAP.3.dll 則通常會在執行舊版 Excel 的工作站上找到。 部分 Analysis Services 功能 (例如 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 增益集) 需要特定版本的 OLE DB 提供者。 如需詳細資訊，請參閱[連接字串屬性 &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)。  
  
##  <a name="bkmk_ADOMD"></a> ADOMD.NET  
 ADOMD.NET 是用於查詢 Analysis Services 資料的 Managed 資料提供者。 Excel 在連接到特定的 Analysis Services Cube 時會使用 ADOMD.NET。 您在 Excel 中所看到的連接字串是指 ADOMD.NET 連接。  
  
 ADOMD.NET 是由 SQL Server 安裝程式所安裝，SQL Server 用戶端應用程式會用它來連接 Analysis Services。 Office 會安裝這個程式庫以支援來自 Excel 的資料連接。 和 SQL Server 中所包含的其他資料提供者一樣，如果您要在自訂程式碼中使用 ADOMD.NET，您可以轉散發此程式庫。 您也可以手動下載及安裝此程式庫以取得較新版本 (請參閱本主題中的 [如何判斷 Analysis Services 資料提供者版本](#bkmk_LibUpdate) )。  
  
 若要查看檔案版本資訊，請在全域組件快取中查找 ADOMD.NET，它在當中是顯示為 `Microsoft.AnalysisServices.AdomdClient`。  
  
 連接到資料庫時，上述三套程式庫的連接字串屬性大致全都相同。 針對 ADOMD.NET 所定義的任何連接字串 (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>)，幾乎也都適用於 AMO 以及 Analysis Services OLE DB 提供者。 如需詳細資訊，請參閱[連接字串屬性 &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)。  
  
 如需有關以程式設計方式連接的詳細資訊，請參閱＜ [Establishing Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)＞。  
  
##  <a name="blkmk_AMO"></a> AMO  
 AMO 是用於伺服器管理及資料定義的 Managed 資料提供者。 例如，SQL Server Management Studio 會使用 AMO 連接到 Analysis Services。  
  
 AMO 是由 SQL Server 安裝程式所安裝，SQL Server 用戶端應用程式會用它來連接 Analysis Services。 您也可以在透過自訂程式碼使用 AMO 時手動下載及安裝此程式庫 (請參閱本主題中的 [如何判斷 Analysis Services 資料提供者版本](#bkmk_LibUpdate) )。 您可以在全域組件快取 (如 `Microsoft.AnalysisServices`) 中找到 AMO。  
  
 使用 AMO 的連接很小，包含 「 資料來源 =\<伺服器名稱 >"。 建立連接之後，您將使用 API 處理資料庫集合與主要物件。 SSDT 和 SSMS 都是使用 AMO 連接到 Analysis Services 執行個體。  
  
 如需有關以程式設計方式連接的詳細資訊，請參閱＜ [Programming AMO Fundamental Objects](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md)＞。  
  
## <a name="see-also"></a>請參閱＜  
 [連接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
