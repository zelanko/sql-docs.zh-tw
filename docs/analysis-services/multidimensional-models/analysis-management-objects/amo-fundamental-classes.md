---
title: "AMO 基礎類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- data sources [AMO]
- AMO, database objects
- AMO, server objects
- Analysis Management Objects, server objects
- database objects [AMO]
- Analysis Management Objects, database objects
- AMO, data sources
- Analysis Management Objects, data sources
ms.assetid: 440e9287-53a2-4db3-9481-1d2ceb6e5b5a
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5323ecb7ac5acc40964357e57ce86f6538313ea9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="amo-fundamental-classes"></a>AMO 基礎類別
  基礎類別是使用分析管理物件 (AMO) 的起點。 透過這些類別，就可以為應用程式內將使用的其餘物件建立環境。 基礎類別包括下列物件：<xref:Microsoft.AnalysisServices.Server>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataSource> 和 <xref:Microsoft.AnalysisServices.DataSourceView>。  
  
 下圖顯示在本主題中說明的類別關聯性。  
  
 ![AMO 基礎類別](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-fundamentalclasses.gif "AMO 基礎類別")  
  
 本主題包含下列幾節：  
  
-   [伺服器物件](#ServerObjects)  
  
-   [資料庫物件](#DatabaseObjects)  
  
-   [DataSource 與 DataSourceView 物件](#DSandDSV)  
  
##  <a name="ServerObjects"></a>伺服器物件  
 此外，您將可以存取下列方法：  
  
-   連接管理：Connect、Disconnect、Reconnect 和 GetConnectionState。  
  
-   交易管理：BeginTransaction，CommitTransaction 和 RollbackTransaction。  
  
-   備份與還原。  
  
-   DDL 執行：Execute、CancelCommand、SendXmlaRequest、StartXmlaRequest。  
  
-   中繼資料管理：UpdateObjects 和 Validate。  
  
 若要連接到伺服器，您需要像在 ADOMD.NET 和 OLEDB 中使用的標準連接字串。 如需詳細資訊，請參閱<xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>。 可以將伺服器的名稱指定為連接字串，而不需要使用連接字串格式。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Server>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
##  <a name="DatabaseObjects"></a>資料庫物件  
 若要在您的應用程式中使用 <xref:Microsoft.AnalysisServices.Database> 物件，您必須從父伺服器資料庫集合中取得資料庫的執行個體。 若要建立資料庫，可以將 <xref:Microsoft.AnalysisServices.Database> 物件加入伺服器資料庫集合，並將新執行個體更新到伺服器。 若要刪除資料庫，可以使用資料庫自己的 Drop 方法來卸除 <xref:Microsoft.AnalysisServices.Database> 物件。  
  
 透過使用 BackUp 方法 (從 <xref:Microsoft.AnalysisServices.Database> 物件或是從 <xref:Microsoft.AnalysisServices.Server> 物件)，可以備份資料庫；但是只能從 <xref:Microsoft.AnalysisServices.Server> 物件的 Restore 方法進行還原。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Database>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
##  <a name="DSandDSV"></a>DataSource 與 DataSourceView 物件  
 透過從資料庫類別使用 <xref:Microsoft.AnalysisServices.DataSourceCollection> 來管理資料來源。 可以使用 <xref:Microsoft.AnalysisServices.DataSource> 物件的 Add 方法來建立 <xref:Microsoft.AnalysisServices.DataSourceCollection> 的執行個體。 可以使用 <xref:Microsoft.AnalysisServices.DataSource> 物件的 Remove 方法來刪除 <xref:Microsoft.AnalysisServices.DataSourceCollection> 的執行個體。  
  
 <xref:Microsoft.AnalysisServices.DataSourceView> 物件是從資料庫類別中的 <xref:Microsoft.AnalysisServices.DataSourceViewCollection> 物件來管理。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.DataSource>＞中的＜<xref:Microsoft.AnalysisServices.DataSourceView>＞與＜<xref:Microsoft.AnalysisServices>＞。  
  
## <a name="see-also"></a>請參閱＜  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 基礎物件的程式設計](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md)  
  
  
