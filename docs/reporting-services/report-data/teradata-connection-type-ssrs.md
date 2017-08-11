---
title: "Teradata 連接類型 (SSRS) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c74e24e12f97d264780e712a1e7e5f3fbea6f9fb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="teradata-connection-type-ssrs"></a>Teradata 連接類型 (SSRS)
  若要在報表中包含來自 Teradata 關聯式資料庫的資料，您必須具有以 Teradata 類型的報表資料來源為基礎的資料集。 此內建的資料來源類型是以 .NET Managed Provider for Teradata 資料處理延伸模組為基礎。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 連接字串  
 請洽詢資料庫管理員，以取得用來連接資料來源的連接資訊和認證。 下列連接字串範例會在使用 IP 位址所指定的伺服器上指定 Teradata 資料庫。  
  
```  
data source=<IP Address>  
```  
  
 如需更多連接字串範例，請參閱 [報表產生器中的資料連接、資料來源及連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
##  <a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 如需詳細資訊，請參閱[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 或[在報表產生器中指定認證](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
  
##  <a name="Remarks"></a> 備註  
 系統管理員必須先安裝支援從 Teradata 資料庫擷取資料的 .NET Data Provider for Teradata 版本，您才能夠連接 Teradata 資料來源。 此資料提供者必須與報表產生器安裝在同一部電腦上，並且同樣位於報表伺服器上。  
  
 這個資料提供者並沒有支援所有的報表傳遞模式。 這個資料處理延伸模組不支援透過資料驅動訂閱所傳遞的報表。 如需詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件集的 [Use an External Data Source for Subscriber Data &#40;Data-Driven Subscription&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) (使用外部資料來源以取得訂閱者資料 (資料驅動訂閱))。  
  
  
##  <a name="Models"></a> 報表模型  
 若要從以 Teradata 資料來源為基礎的報表模型建立資料集，該模型必須是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的模型設計師中所設計，而且在報表伺服器上發行。  
  
  
##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [資料連接、 資料來源和報表產生器中的連接字串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供資料集查詢所產生之欄位集合的相關資訊。  
  
 《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [線上叢書](http://go.microsoft.com/fwlink/?linkid=121312)》中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  
  
 [使用 SQL Server 2008 Reporting Services 搭配 .NET Framework Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkID=130848)  
 提供有關使用這個資料延伸模組的詳細資訊。  
  
  
## <a name="see-also"></a>請參閱＜  
 [報表參數 &#40;報表產生器和報表設計工具 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、 群組和排序資料 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
