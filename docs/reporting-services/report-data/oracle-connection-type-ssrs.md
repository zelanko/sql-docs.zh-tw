---
title: "Oracle 連接類型 (SSRS) |Microsoft 文件"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4ce6a83437433c2254b2993f68f78e8c8c8f4375
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="oracle-connection-type-ssrs"></a>Oracle 連接類型 (SSRS)
若要在報表中使用來自 Oracle 資料庫的資料，您必須具有以 Oracle 類型的報表資料來源為基礎的資料集。 此內建資料來源類型會直接使用 Oracle 資料提供者，且需要 Oracle 用戶端軟體元件。

若要安裝 Oracle 用戶端工具可以執行下列作業。
 
1.  移至[Oracle 的下載網站](http://www.oracle.com/us/products/tools/index-090165.html)
2.  下載適用於 Windows （64 位元的伺服器，工具的 32 位元） ODAC 12c 版本 4 (12.1.0.2.4)
3.  安裝.NET 4 的資料提供者
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 連接字串  
 請洽詢資料庫管理員，以取得用來連接資料來源的連接資訊和認證。 下列連接字串範例會使用 Unicode 來指定名為 "Oracle9" 之伺服器上的 Oracle 資料庫。 伺服器名稱必須符合 Tnsnames.ora 組態檔中定義為 Oracle 伺服器執行個體名稱的內容。  
  
```  
Data Source="Oracle"; Unicode="True"  
```  
  
 如需連接字串範例的詳細資訊，請參閱 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
##  <a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 如需詳細資訊，請參閱[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 或[在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
  
##  <a name="Query"></a> 查詢  
 若要建立資料集，您可以從下拉式清單中選取預存程序，或是建立 SQL 查詢。 若要建立查詢，您必須使用以文字為基礎的查詢設計工具。 如需詳細資訊，請參閱[文字為基礎的查詢設計工具使用者介面 &#40;報表產生器 &#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 您可以指定只傳回一個結果集的預存程序。 不支援使用以資料指標為基礎的查詢。  
  
##  <a name="Parameters"></a> 參數  
 如果查詢包含查詢變數，就會自動產生對應的報表參數。 此延伸模組支援具名參數。 若使用 Oracle 9 或更新版本，則支援多重值的參數。  
  
 報表參數是透過預設屬性值建立，您可能會需要修改這些值。 例如，每一個報表參數的資料類型都是 **[文字]**。 建立報表參數後，您可能必須變更預設值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
  
##  <a name="Remarks"></a> 備註  
 系統管理員必須先安裝支援從 Oracle 資料庫擷取資料的 .NET Data Provider for Oracle 版本，您才能夠連接 Oracle 資料來源。 此資料提供者必須與報表產生器安裝在同一部電腦上，並且同樣位於報表伺服器上。  
  
 如需詳細資訊，請參閱下列內容：  
  
-   msdn.microsoft.com 上的[使用 Oracle 的 .NET Framework 資料提供者](http://go.microsoft.com/fwlink/?LinkId=112314)   
  
-   [如何使用 Reporting Services 設定及存取 Oracle 資料來源 (機器翻譯)](http://support.microsoft.com/kb/834305)  
  
-   [如何新增 NETWORK SERVICE 安全性主體的權限 (機器翻譯)](http://support.microsoft.com/kb/870668)  
  
###### <a name="alternate-data-extensions"></a>替代資料延伸模組  
 您也可以使用 OLE DB 資料來源類型，從 Oracle 資料庫擷取資料。 如需詳細資訊，請參閱 [OLE DB 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)。  
  
###### <a name="report-models"></a>報表模型  
 您也可以根據 Oracle 資料庫建立模型。  
  
###### <a name="platform-and-version-information"></a>平台和版本資訊  
 如需平台和版本支援的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ 線上叢書》](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 如何主題  
 本節包含使用資料連接、資料來源與資料集的逐步指示。  
  
 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [將篩選加入資料集 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [資料連接、 資料來源和報表產生器中的連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供查詢所產生之資料集欄位集合的相關資訊。  
  
 《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書》](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  
  
  
## <a name="see-also"></a>請參閱＜  
 [報表參數 &#40;報表產生器和報表設計工具 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、 群組和排序資料 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

