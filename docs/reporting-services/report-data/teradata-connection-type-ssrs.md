---
title: Teradata 連線類型 | Microsoft Docs
description: 請使用本文中 Teradata 連線類型的相關資訊，了解如何建置資料來源。
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a97d0320affe87e039f4369d699f1998caa8d153
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458311"
---
# <a name="teradata-connection-type-ssrs"></a>Teradata 連接類型 (SSRS)
  若要在報告中包含 Teradata 的資料，您必須有以類型 Teradata 報告資料來源為基礎的資料集。 此內建的資料來源類型是以 .NET Managed Provider for Teradata 資料處理延伸模組為基礎。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 [加入及驗證資料連接 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="connection-string"></a><a name="Connection"></a> 連接字串  
 請洽詢資料庫管理員，以取得用來連接資料來源的連接資訊和認證。 下列連接字串範例會在使用 IP 位址所指定的伺服器上指定 Teradata 資料來源：  
  
```  
data source=<IP Address>  
```  
  
 如需詳細的連接字串範例，請參閱[建立資料連接字串 - 報表產生器 & SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
##  <a name="credentials"></a><a name="Credentials"></a> 認證  
 需要有認證才能夠執行報表、於本機預覽報表並且從報表伺服器預覽報表。  
  
 發行報表之後，您可能需要變更資料來源的認證，如此當報表在報表伺服器上執行時，擷取資料的權限就會是有效的。  
  
 如需詳細資訊，請參閱[建立資料連接字串 - 報表產生器 & SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 或[指定報表資料來源的認證及連接資訊](specify-credential-and-connection-information-for-report-data-sources.md)。  
  
  
##  <a name="remarks"></a><a name="Remarks"></a> 備註  
 系統管理員必須先安裝支援從 Teradata 擷取資料的 .NET Data Provider for Teradata 版本，您才能夠將 Teradata 資料來源連線。 此資料提供者必須與報表產生器安裝在同一部電腦上，並且同樣位於報表伺服器上。  
  
 這個資料提供者並沒有支援所有的報表傳遞模式。 這個資料處理延伸模組不支援透過資料驅動訂閱所傳遞的報表。 如需詳細資訊，請參閱[使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
  
##  <a name="report-models"></a><a name="Models"></a> 報表模型  
 若要從以 Teradata 資料來源為基礎的報表模型建立資料集，該模型必須是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的模型設計師中所設計，並在報表伺服器上發佈。  
  
  
##  <a name="related-sections"></a><a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [建立資料連接字串 - 報表產生器及 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供資料集查詢所產生之欄位集合的相關資訊。  
  
 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) 提供各資料延伸模組的平台與版本支援詳細資訊。  
 
  
## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
