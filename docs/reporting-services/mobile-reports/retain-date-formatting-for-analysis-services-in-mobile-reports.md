---
title: 保留行動報表中 Analysis Services 的日期格式 | Microsoft Docs
description: 在行動報表發行工具中，將量值新增至報表產生器中的共用資料集，讓 Analysis Services 資料來源中的日期可以保留其資料類型。
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e9a9a199-40e3-4381-b250-1b99fb83aa62
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5fef66452820975107e06e20a4085978163d957d
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907076"
---
# <a name="retain-date-formatting-for-analysis-services-in-mobile-reports"></a>保留行動報表中 Analysis Services 的日期格式
在報表產生器中將量值加入共用資料集中，讓 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 資料來源中的日期在 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]中保留其資料類型。

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 查詢的預設傳回類型是字串。  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 報表產生器中建立資料集時，會使用字串類型，並將其儲存至伺服器。 

不過，當 JSON 資料表轉譯器處理資料集時，會將資料行的值讀取為字串，並轉譯字串。  接著， [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 提取資料表時，也只會看到字串。

在報表產生器中建立共用資料集時，此問題的因應措施是加入導出成員。 它適用於 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 多維度和表格式模型。

## <a name="create-a-measure-to-retain-a-date-field-data-type"></a>建立量值來保留日期欄位資料類型

1. 建立量值以保留有問題之日期欄位的值，然後在運算式欄位中，選擇日期的階層/層級，並附加 **.CurrentMember.MemberValue** 。 例如：
 
   [Internet Sales].[Ship Date].CurrentMember.MemberValue
   
   ![已標註 [運算式] 文字方塊的 [導出成員產生器] 對話方塊螢幕擷取畫面。](../../reporting-services/mobile-reports/media/ssas-calculated-member-report-builder.png)
   
2. 現在您可以將此導出成員附加至這組資料行，方法是將它從左下方的 [導出成員] 清單拖放至右邊的資料行方格。  

   ![已標註 [導出成員] 區段的查詢設計工具螢幕擷取畫面。](../../reporting-services/mobile-reports/media/ssas-query-designer-calculated-member-report-builder.png) 
   
### <a name="see-also"></a>另請參閱

-  [Reporting Services 行動報表資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)
-  [準備 Reporting Services 行動報表的資料](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)
