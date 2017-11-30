---
title: "資料集屬性對話方塊、選項 (報表產生器) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10020"
- sql13.rtp.rptdesigner.datasetproperties.options.f1
- "10130"
ms.assetid: 43e50133-45ef-47a2-b575-34dfcc28ec98
caps.latest.revision: "15"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 0425449331af8a4bb6d26203447bcb1fed0aaac2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="dataset-properties-dialog-box-options-report-builder"></a>資料集屬性對話方塊、選項 (報表產生器)
  選取 [資料集屬性] 對話方塊上的 [選項] 來變更查詢的資料選項，例如定序選項以及將小計視為詳細資料。 如需定序的詳細資訊，請參閱《 [SQL Server 線上叢書](../../relational-databases/collations/collation-and-unicode-support.md) 》中的 [定序與 Unicode 支援](http://go.microsoft.com/fwlink/?linkid=98335)。  
  
 屬於報表伺服器上共用資料集定義之一部分的資料選項會影響所有使用共用資料集的報表。 當共用資料集加入至報表之後，您可以覆寫它的選項。 這些變更只會影響其定義所在的報表。  
  
 內嵌資料集的資料選項只會影響其定義所在的報表。  
  
 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="options"></a>選項。  
 **定序**  
 選取決定排序資料所用之定序順序的地區設定。 **[預設值]** 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果無法衍生此值，則從電腦的地區設定衍生預設值。  
  
 **區分大小寫**  
 選取決定區分大小寫的值。 此選項指出資料是否區分大小寫。 您可以將 **[區分大小寫]** 設定為 **[True]**、 **[False]**或 **[Auto]**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分大小寫類型，報表會以該值為 **False**來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **區分腔調字**  
 選取決定區分腔調字的值。 **[區分腔調字]** 指出資料是否區分腔調字，而且可以設定為 **[True]**、 **[False]**或 **[Auto]**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分腔調字類型，報表會以該值為 **[False]**來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **區分假名**  
 選取決定區分假名的值。 此選項指出資料是否區分假名；它可以設定為 **[True]**、 **[False]**或 **[Auto]**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分假名類型，報表會以該值為 **[False]**來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **區分全半形**  
 選取決定區分全半形的值。 此選項指出資料是否區分全半形，而且可以設定為 **True**、 **False**或 **Auto**。預設值 [Auto] 指出報表伺服器應該在報表執行時，嘗試從資料提供者衍生此值。 如果資料提供者不支援區分全半形類型，報表會以該值為 **[False]**來執行。 如果您知道值，而且知道系統支援該值，選擇 **[True]**。  
  
 **將小計當做詳細資料列**  
 選取一個值，指出您是否要讓小計資料列當做詳細資料列而非彙總資料列。 如果報表不使用 **Aggregate**() 函數來存取資料集中的任何欄位，預設值 **Auto**表示小計資料列應視為詳細資料列。 如果您要讓小計資料列當做彙總資料列，選擇 **[False]**。 如果您要讓小計資料列當作詳細資料列，而且您知道它們不使用 **Aggregate**() 函數，請選擇 **True**。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和精靈的報表產生器說明](http://msdn.microsoft.com/en-us/2da24891-0b6d-4d3c-8b18-81b98752642f)   
 [彙總函式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [資料集屬性對話方塊、查詢 &#40;報表產生器&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md)  
  
  
