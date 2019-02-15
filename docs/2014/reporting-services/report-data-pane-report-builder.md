---
title: 報表資料窗格 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 369540d7d3c75a781c338cf5d172fa82b16df7c7
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290056"
---
# <a name="report-data-pane-report-builder"></a>報表資料窗格 (報表產生器)
  [報表資料] 窗格可用於檢視報表中目前定義的參數、資料來源、資料集、欄位集合和影像。 [圖表資料] 會以階層檢視來顯示表示報表中資料的項目。 最上層節點代表內建欄位、參數、影像和資料來源參考。 請展開每個節點以檢視資料項目。 例如，當您展開資料來源節點時，為該資料來源所定義的資料集就會顯示。 在展開資料集時，其欄位集合就會顯示。 您可以將項目拖曳至報表設計介面或 [群組] 窗格，以便連結資料與報表頁面上的選取報表項目。 如需詳細資訊，請參閱[報表設計檢視 &#40;報表產生器&#41;](report-builder/report-design-view-report-builder.md)。  
  
## <a name="options"></a>選項。  
 **內建欄位**  
 代表報表中的常用欄位，例如：報表名稱或頁碼。 如需詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)。  
  
 **參數**  
 代表報表參數的集合，每個參數都可以是單一數值或多重值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  
  
 **影像**  
 代表用於報表中的一組影像。 如需詳細資訊，請參閱[影像 &#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)。  
  
 **資料來源**  
 代表內嵌資料來源或共用資料來源的參考。 資料來源代表報表資料的來源。 資料來源就是使用它之資料集集合的父節點。 如需詳細資訊，請參閱 <<c0> [ 將資料加入至報表&#40;報表產生器及 SSRS&#41; ](report-data/report-datasets-ssrs.md)並[資料連接、 資料來源和報表產生器中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)。</c0>  
  
 **資料集**  
 代表透過執行單一命令，從資料來源中擷取的資料，例如從 [!INCLUDE[tsql](../includes/tsql-md.md)] 資料庫中擷取資料的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢。 資料集是由查詢所指定之欄位集合的父節點，也包括導出欄位。 報表產生器支援查詢設計工具，可協助您指定查詢。 如需詳細資訊，請參閱 <<c0> [ 將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [群組窗格 &#40;報表產生器&#41;](report-design/grouping-pane-report-builder.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
