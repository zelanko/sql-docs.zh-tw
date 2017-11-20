---
title: "以程式設計方式建立封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 7474b1f4-7607-4f28-a6fd-67f7db1dd3f8
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b80495b726ac6fdac713ba028629633bf84cc004
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="building-packages-programmatically"></a>以程式設計方式建立封裝
  如果您需要動態建立封裝，或要在開發環境以外的地方管理和執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，可以使用程式設計方式操作封裝。 在這種方法中，您有連續範圍的選項：  
  
-   在不須修改的情況下載入並執行現有的封裝。  
  
-   載入現有的封裝、重新加以設定 (例如，針對不同的資料來源)，然後執行。  
  
-   建立新封裝、逐物件和逐屬性地加入與設定元件、儲存，然後加以執行。  
  
 您可以透過任何 Managed 程式語言，使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 物件模型撰寫用來建立、設定和執行封裝的程式碼。 例如，您可能會想要建立中繼資料驅動的封裝，以根據選取的資料來源及其資料表與資料行，設定其連接或是其資料來源、轉換與目的地。  
  
 本節會描述和示範如何以程式設計方式逐行建立和設定封裝。 在較不複雜的封裝程式設計選項範圍的結束時，您可以只載入和執行而不需修改現有的封裝中所述[執行以程式設計方式管理封裝](../../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)。  
  
 並未在此說明的中間選項是以範本形式載入現有的封裝、重新加以設定 (例如，針對不同的資料來源)，然後執行。 您也可以使用本節中的資訊，修改封裝中的現有物件。  
  
> [!NOTE]  
>  當您使用現有封裝做為範本，並修改資料流程中的現有資料行時，可能必須移除現有的資料行，並呼叫受影響元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法。  
  
## <a name="in-this-section"></a>섹션 내용  
 [以程式設計方式建立封裝](../../integration-services/building-packages-programmatically/creating-a-package-programmatically.md)  
 描述如何以程式設計方式建立封裝。  
  
 [以程式設計方式加入工作](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
 描述如何將工作加入封裝。  
  
 [以程式設計方式連接工作](../../integration-services/building-packages-programmatically/connecting-tasks-programmatically.md)  
 描述如何根據上一個工作或容器的執行結果，來控制封裝中容器和工作的執行。  
  
 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)  
 描述如何將連接管理員加入封裝。  
  
 [以程式設計方式使用變數](../../integration-services/building-packages-programmatically/working-with-variables-programmatically.md)  
 描述如何在封裝執行期間加入和使用變數。  
  
 [以程式設計方式處理事件](../../integration-services/building-packages-programmatically/handling-events-programmatically.md)  
 描述如何處理封裝和工作事件。  
  
 [啟用以程式設計方式記錄](../../integration-services/building-packages-programmatically/enabling-logging-programmatically.md)  
 描述如何為封裝或工作啟用記錄，以及如何將自訂篩選套用至記錄事件。  
  
 [以程式設計方式加入資料流程工作](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
 描述如何加入及設定資料流程工作和其元件。  
  
 [以程式設計方式探索資料流程元件](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
 描述如何偵測在本機電腦上安裝的元件。  
  
 [以程式設計方式加入資料流程元件](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
 描述如何將元件加入資料流程工作。  
  
 [以程式設計方式連接資料流程元件](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
 描述如何連接兩個資料流程元件。  
  
 [以程式設計方式選取輸入資料行](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
 描述如何從那些由資料流程中的上游元件提供給元件的輸入資料行進行選取。  
  
 [以程式設計方式儲存封裝](../../integration-services/building-packages-programmatically/saving-a-package-programmatically.md)  
 描述如何以程式設計方式儲存封裝。  
  
## <a name="reference"></a>참조  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)  
 列出預先定義的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 錯誤碼，以及其符號名稱與描述。  
  
## <a name="related-sections"></a>相關章節  
 [使用指令碼擴充封裝](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 討論如何透過使用指令碼工作擴充控制流程，或是如何透過使用指令碼元件擴充資料流程。  
  
 [使用自訂物件擴充封裝](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 討論如何建立程式自訂工作、資料流程元件以及其他封裝物件，以供在多個封裝中使用。  
  
 [執行和以程式設計方式管理封裝](../../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 討論如何列舉、執行和管理封裝以及儲存封裝的資料夾。  
  
## <a name="external-resources"></a>外部資源  
  
-   CodePlex 範例： [Integration Services 產品範例](http://go.microsoft.com/fwlink/?LinkID=131204)，位於 www.codeplex.com/MSFTISProdSamples  
  
-   部落格文章：[效能剖析自訂擴充功能](http://go.microsoft.com/fwlink/?LinkId=238831)，blogs.msdn.com 上。  

## <a name="see-also"></a>另請參閱  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  

