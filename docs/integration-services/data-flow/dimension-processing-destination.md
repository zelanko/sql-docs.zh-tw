---
title: 維度處理目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dimensionprocessingdest.f1
- sql13.dts.designer.dimprocessingtransformation.connection.f1
- sql13.dts.designer.dimprocessingtransformation.mappings.f1
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 257f4ebaba273ad465c259a9bdd633e6513cda53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726946"
---
# <a name="dimension-processing-destination"></a>維度處理目的地

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「維度處理」目的地會載入及處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 維度。 如需維度的詳細資訊，請參閱[維度 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)。  
  
 「維度處理」目的地包含下列功能：  
  
-   執行累加式、完整或更新處理的選項。  
  
-   錯誤組態，可以指定在發生指定數目的錯誤之後，維度處理是忽略錯誤還是停止。  
  
-   將輸入資料行對應至維度資料表中的資料行。  
  
 如需處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>設定維度處理目的地  
 「維度處理」目的地會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接管理員，以連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或包含目的地所處理之維度的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 此目的地擁有一個輸入。 它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="dimension-processing-destination-editor-connection-manager-page"></a>維度處理目的地編輯器 (連接管理員頁面)
  使用 **[維度處理目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 計畫的連接或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之執行個體的連接。  
  
### <a name="options"></a>選項。  
 **[ODBC 目的地編輯器]**  
 從清單中選取現有的連接管理員，或按一下 [新增]  來建立新的連接管理員。  
  
 **新增**  
 使用 [加入 Analysis Services 連接管理員]  對話方塊來建立新的連接。  
  
 **可用維度清單**  
 選取要處理的維度。  
  
 **處理方法**  
 選取要套用至清單中選取之維度的處理方法。 此選項的預設值是 **[完整]** 。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**加入 (累加)**|執行維度的累加處理。|  
|**[完整]**|執行維度的完整處理。|  
|**Update**|執行維度的更新處理。|  
  
## <a name="dimension-processing-destination-editor-mappings-page"></a>維度處理目的地編輯器 (對應頁面)
  使用 **[維度處理目的地編輯器]** 對話方塊的 **[對應]** 頁面，即可將輸入資料行對應至維度資料行。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 使用拖放作業，即可將資料表中的可用輸入資料行對應到目的地資料行。  
  
 **可用的目的地資料行**  
 檢視可用的目的地資料行清單。 使用拖放作業，即可將資料表中的可用目的地資料行對應到輸入資料行。  
  
 **輸入資料行**  
 從上述資料表檢視選取的輸入資料行。 您可以使用 **[可用的輸入資料行]** 清單來變更對應。  
  
 **目的地資料行**  
 檢視每個可用的目的地資料行，不論是否已經對應。  
  
## <a name="dimension-processing-destination-editor-advanced-page"></a>維度處理目的地編輯器 (進階頁面)
  使用 **[維度處理目的地編輯器]** 對話方塊的 **[進階]** 頁面，來設定錯誤處理。  
  
### <a name="options"></a>選項。  
 **使用預設錯誤組態。**  
 指定是否要使用預設的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 錯誤處理。 依預設，此值為 **True**。  
  
 **索引鍵錯誤動作**  
 指定如何處理具有無法接受之索引鍵值的記錄。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|將無法接受的索引鍵值轉換為 **UnknownMember** 值。|  
|**DiscardRecord**|捨棄記錄。|  
  
 **忽略錯誤**  
 指定應該忽略的錯誤。  
  
 **發生錯誤時停止**  
 指定發生錯誤時，應該停止處理。  
  
 **錯誤數目**  
 如果您已選取 [發生錯誤時停止]  ，則指定處理應該停止的錯誤臨界值。  
  
 **發生錯誤時要執行的動作**  
 如果您已選取 [發生錯誤時停止]  ，則指定到達錯誤臨界值時要採取的動作。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**StopProcessing**|停止處理。|  
|**StopLogging**|停止記錄錯誤。|  
  
 **找不到索引鍵**  
 針對找不到索引鍵錯誤，指定要採取的動作。 依預設，此值為 **ReportAndContinue**。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **重複的索引鍵**  
 針對重複索引鍵錯誤，指定要採取的動作。 依預設，此值為 **IgnoreError**。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **Null 索引鍵已轉換為未知**  
 指定當 Null 索引鍵轉換為 **UnknownMember** 值的時候應採取的動作。 依預設，此值為 **IgnoreError**。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **不允許 Null 索引鍵**  
 指定在不允許 Null 索引鍵的情況下如果發現 Null 索引鍵，所要採取的動作。 依預設，此值為 **ReportAndContinue**。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**IgnoreError**|忽略錯誤並繼續處理。|  
|**ReportAndContinue**|報告錯誤並繼續處理。|  
|**ReportAndStop**|報告錯誤並停止處理。|  
  
 **錯誤記錄路徑**  
 輸入錯誤記錄路徑，或者按一下 [瀏覽 (…)]  按鈕以選取目的地。  
  
 **瀏覽 (...)**  
 選取錯誤記錄的路徑。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
