---
title: 資料連接、 資料來源和報表產生器中的連接字串 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10421"
ms.assetid: 7e103637-4371-43d7-821c-d269c2cc1b34
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5821d8d747609abfc8433a3ff9ad0ecf2676be7d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011010"
---
# <a name="data-connections-data-sources-and-connection-strings-in-report-builder"></a>報表產生器中的資料連接、資料來源及連接字串
  若要在報表中包含資料，請建立資料連接和資料集。 資料連接包括如何存取外部資料來源的相關資訊。 資料集包括查詢命令，其中指定要使用資料連接包含哪些資料。  
  
1.  **報表資料窗格中的資料來源** ：在您建立內嵌資料來源或加入共用資料來源之後，[報表資料] 窗格中就會出現資料來源。  
  
2.  **連接對話方塊** ：使用 [連接對話方塊] 可建立連接字串或貼上連接字串。  
  
3.  **資料連接資訊** ：連接字串會傳遞至資料延伸模組。  
  
4.  **認證** ：認證會與連接字串分開管理。  
  
5.  **資料延伸模組/資料提供者** ：資料可經由多個資料存取層連接。  
  
6.  **外部資料來源** ：從關聯式資料庫、多維資料庫、SharePoint 清單、Web 服務或報表模型擷取資料。  
  
 如需詳細資訊，請參閱 <<c0> [ 內嵌和共用資料連接或資料來源&#40;報表產生器及 SSRS&#41; ](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)並[資料 Connections、 Data Sources，and Connection Strings in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).</c0>  
  
 資料也可以併入報表中，其方式是使用預先定義的共用資料來源、共用資料集和報表組件。 這些項目已經有您所需的資料連接資訊。 如需詳細資訊，請參閱 <<c0> [ 將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)。</c0>  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 ![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")  
  
##  <a name="ConnectionString"></a> 連接字串範例  
 資料連接包含連接字串，這個字串通常是由外部資料來源的擁有者所提供。 下表列出各種不同外部資料來源類型的連接字串範例。  
  
|**資料來源**|**範例**|**說明**|  
|---------------------|-----------------|---------------------|  
|本機伺服器上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫|`data source="(local)";initial catalog=AdventureWorks2012`|將資料來源類型設定為 `SQL Server`。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體資料庫|`Data Source=localhost\MSSQL12.InstanceName; Initial Catalog= AdventureWorks2012`|將資料來源類型設定為 `SQL Server`。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 資料庫|`Data Source=localhost\MSSQL12.SQLEXPRESS; Initial Catalog= AdventureWorks2012`|將資料來源類型設定為 `SQL Server`。|  
|本機伺服器上的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫|`data source=localhost;initial catalog=Adventure Works DW 2012`|將資料來源類型設定為 `SQL Server Analysis Services`。|  
|SharePoint 清單|`data source=http://MySharePointWeb/MySharePointSite/`|將資料來源類型設定為 `SharePoint List`。|  
||||  
|報表模型|不適用。|您不需要報表模型的連接字串。 在報表產生器中，瀏覽至報表伺服器，並選取報表模型 .smdl 檔案。|  
|Oracle 伺服器|`data source=myserver`|將資料來源類型設定為 `Oracle`。 Oracle 用戶端工具必須安裝在報表產生器電腦和報表伺服器上。|  
|SAP NetWeaver BI 資料來源|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|將資料來源類型設定為 `SAP NetWeaver BI`。|  
|Hyperion Essbase 資料來源|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|將資料來源類型設定為 `Hyperion Essbase`。|  
|Teradata 資料來源|`data source=` *\<NN>.\<NNN>.\<NNN>.\<N>* `;`|將資料來源類型設定為 `Teradata`。 連接字串是四個欄位形式的網際網路通訊協定 (IP) 位址，其中每個欄位都可以是 1 到 3 位數。|  
|Teradata 資料來源|`Database=` \<資料庫名稱> `; data source=` *\<NN*N *>.\<NNN>.\<NNN>.\<N*NN*>*`;Use X Views=False;Restrict to Default Database=True`|與前述範例類似，將資料來源類型設定為 `Teradata`。 請只使用在 Database 標記中指定的預設資料庫，而不要自動探索資料關聯性。|  
|XML 資料來源, Web 服務|`data source=http://adventure-works.com/results.aspx`|將資料來源類型設定為 `XML`。 連接字串是支援 Web 服務定義語言 (WSDL) 之 Web 服務的 URL。|  
|XML 資料來源、XML 文件|`http://localhost/XML/Customers.xml`|將資料來源類型設定為 `XML`。 連接字串是 XML 文件的 URL。|  
|XML 資料來源, 內嵌 XML 文件|*Empty*|將資料來源類型設定為 `XML`。 XML 資料內嵌在報表定義中。|  
  
 如需有關每個連接類型的詳細資訊，請參閱 <<c0> [ 從外部資料來源加入資料&#40;SSRS&#41; ](report-data/add-data-from-external-data-sources-ssrs.md)並[Reporting Services 所支援的資料來源&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)。</c0>  
  

  
##  <a name="Creating"></a> 建立資料來源  
 若要建立內嵌資料來源，您必須具有存取資料所需的連接字串和認證。 這項資訊通常是來自於資料來源的擁有者。 資料連接會儲存在報表定義中，當做資料來源的一部分。 認證會與連接分開管理。 如需逐步指示，請參閱 <<c0> [ 加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。</c0>  
  
> [!NOTE]  
>  某些認證類型可能不支援報表產生器所使用的所有情況：若要在查詢設計工具內執行查詢，請在未連接報表伺服器時從電腦預覽報表，然後從報表伺服器執行報表。 我們建議您盡可能使用共用資料來源。 您也可以將共用資料來源的認證儲存在報表伺服器上。 如需詳細資訊，請參閱 [在報表產生器中指定認證](../../2014/reporting-services/specify-credentials-in-report-builder.md)。  
  
 若要建立共用的資料來源，您必須使用報表管理員直接在報表伺服器上建立資料來源，或使用類似報表設計師中撰寫環境[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 建立內嵌或共用資料來源 &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)。</c0>  
  

  
## <a name="see-also"></a>另請參閱  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [報表組件 &#40;報表產生器及 SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
