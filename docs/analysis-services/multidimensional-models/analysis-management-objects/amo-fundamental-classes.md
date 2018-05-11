---
title: AMO 基礎類別 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 936b092684c8ab8a857b57fa88e2905b8efb0ffd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="amo-fundamental-classes"></a>AMO 基礎類別
  基礎類別是使用分析管理物件 (AMO) 的起點。 透過這些類別，就可以為應用程式內將使用的其餘物件建立環境。 基礎類別包括下列物件：<xref:Microsoft.AnalysisServices.Server>、<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataSource> 和 <xref:Microsoft.AnalysisServices.DataSourceView>。  
  
 下圖顯示在本主題中說明的類別關聯性。  
  
 ![AMO 基礎類別](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-fundamentalclasses.gif "AMO 基礎類別")  
  
 本主題包含下列幾節：  
  
-   [伺服器物件](#ServerObjects)  
  
-   [資料庫物件](#DatabaseObjects)  
  
-   [DataSource 與 DataSourceView 物件](#DSandDSV)  
  
##  <a name="ServerObjects"></a> 伺服器物件  
 此外，您將可以存取下列方法：  
  
-   連接管理：Connect、Disconnect、Reconnect 和 GetConnectionState。  
  
-   交易管理：BeginTransaction，CommitTransaction 和 RollbackTransaction。  
  
-   備份與還原。  
  
-   DDL 執行：Execute、CancelCommand、SendXmlaRequest、StartXmlaRequest。  
  
-   中繼資料管理：UpdateObjects 和 Validate。  
  
 若要連接到伺服器，您需要像在 ADOMD.NET 和 OLEDB 中使用的標準連接字串。 如需詳細資訊，請參閱<xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>。 可以將伺服器的名稱指定為連接字串，而不需要使用連接字串格式。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Server>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
##  <a name="DatabaseObjects"></a> 資料庫物件  
 若要在您的應用程式中使用 <xref:Microsoft.AnalysisServices.Database> 物件，您必須從父伺服器資料庫集合中取得資料庫的執行個體。 若要建立資料庫，可以將 <xref:Microsoft.AnalysisServices.Database> 物件加入伺服器資料庫集合，並將新執行個體更新到伺服器。 若要刪除資料庫，可以使用資料庫自己的 Drop 方法來卸除 <xref:Microsoft.AnalysisServices.Database> 物件。  
  
 透過使用 BackUp 方法 (從 <xref:Microsoft.AnalysisServices.Database> 物件或是從 <xref:Microsoft.AnalysisServices.Server> 物件)，可以備份資料庫；但是只能從 <xref:Microsoft.AnalysisServices.Server> 物件的 Restore 方法進行還原。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.Database>＞中的＜<xref:Microsoft.AnalysisServices>＞。  
  
##  <a name="DSandDSV"></a> DataSource 與 DataSourceView 物件  
 透過從資料庫類別使用 <xref:Microsoft.AnalysisServices.DataSourceCollection> 來管理資料來源。 可以使用 <xref:Microsoft.AnalysisServices.DataSource> 物件的 Add 方法來建立 <xref:Microsoft.AnalysisServices.DataSourceCollection> 的執行個體。 可以使用 <xref:Microsoft.AnalysisServices.DataSource> 物件的 Remove 方法來刪除 <xref:Microsoft.AnalysisServices.DataSourceCollection> 的執行個體。  
  
 <xref:Microsoft.AnalysisServices.DataSourceView> 物件是從資料庫類別中的 <xref:Microsoft.AnalysisServices.DataSourceViewCollection> 物件來管理。  
  
 如需有關可用之方法和屬性的詳細資訊，請參閱＜<xref:Microsoft.AnalysisServices.DataSource>＞中的＜<xref:Microsoft.AnalysisServices.DataSourceView>＞與＜<xref:Microsoft.AnalysisServices>＞。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [程式設計 AMO 基礎物件](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md)  
  
  
