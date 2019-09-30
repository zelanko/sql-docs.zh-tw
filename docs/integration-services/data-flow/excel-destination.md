---
title: Excel 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 418d3c214f667807df997902f97bfa271c8c4742
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292823"
---
# <a name="excel-destination"></a>Excel 目的地

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Excel 目的地會將資料載入至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿中的工作表或範圍。  

> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。
  
## <a name="access-modes"></a>存取模式  
 Excel 目的地提供三種不同的資料存取模式用於載入資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
## <a name="configure-the-excel-destination"></a>設定 Excel 目的地  
 Excel 目的地會使用 Excel 連接管理員，以連接到資料來源，而連接管理員會指定要使用的活頁簿檔案。 如需詳細資訊，請參閱 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
 Excel 目的地擁有一個規則輸入與一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之所有屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 自訂屬性](../../integration-services/data-flow/excel-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Excel 目的地編輯器 (連接管理員頁面)
  使用 **[Excel 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，來指定資料來源資訊，以及預覽結果。 Excel 目的地會將資料載入 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿中的工作表或具名範圍。  
  
> [!NOTE]  
>  在 **[Excel 目的地編輯器]** 中無法使用 Excel 目的地的 **CommandTimeout**屬性，但可使用 **[進階編輯器]** 來設定這個屬性。 此外， **[進階編輯器]** 中只會有特定的快速載入選項。 如需有關這個屬性的詳細資訊，請參閱＜ [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)＞的＜Excel 目的地＞一節。  
  
### <a name="static-options"></a>靜態選項  
 **Excel 連接管理員**  
 從清單中選取現有的 Excel 連線管理員，或按一下 [新增]  建立新的連線管理員。  
  
 **新增**  
 使用 [Excel 連線管理員]  對話方塊來建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|選項|Description|  
|------------|-----------------|  
|資料表或檢視|將資料載入 Excel 資料來源中的工作表或具名範圍。|  
|資料表名稱或檢視名稱變數|在變數中指定工作表或範圍名稱。<br /><br /> **相關資訊**：[在套件中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL (命令)|使用 SQL 查詢將資料載入 Excel 目的地。|  
  
 **Excel 工作表的名稱**  
 從下拉式清單中選取 Excel 目的地。 如果此清單為空，請按一下 **[新增]** 。  
  
 **新增**  
 按一下 [新增]  以啟動 [建立工資料表]  對話方塊。 按一下 **[確定]** 時，對話方塊會建立 **[Excel 連接管理員]** 指向的 Excel 檔案。  
  
 **檢視現有的資料**  
 使用 [預覽查詢結果]  對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
### <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
  
#### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **Excel 工作表的名稱**  
 從資料來源裡可用的資訊清單中，選取工作表或具名範圍的名稱。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 選取包含工作表名稱或具名範圍的變數。  
  
#### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢的文字，按一下 [建立查詢]  來建立查詢，或是按一下 [瀏覽]  以找出包含查詢文字的檔案。  
  
 **建立查詢**  
 使用 [查詢產生器]  對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟]  對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
## <a name="excel-destination-editor-mappings-page"></a>Excel 目的地編輯器 (對應頁面)
  使用 **[Excel 目的地編輯器]** 對話方塊的 **[對應]** 頁面，將輸入資料行對應至目的地資料行。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 使用拖放作業，即可將資料表中的可用輸入資料行對應到目的地資料行。  
  
 **可用的目的地資料行**  
 檢視可用的目的地資料行清單。 使用拖放作業，即可將資料表中的可用目的地資料行對應到輸入資料行。  
  
 **輸入資料行**  
 從上述資料表檢視選取的輸入資料行。 您可以使用 **[可用的輸入資料行]** 清單來變更對應。  
  
 **目的地資料行**  
 檢視每個可用的目的地資料行，不論是否已經對應。  
  
## <a name="excel-destination-editor-error-output-page"></a>Excel 目的地編輯器 (錯誤輸出頁面)
  使用 [Excel 目的地編輯器]  對話方塊的 [進階]  頁面，即可指定錯誤處理的選項。  
  
### <a name="options"></a>選項。  
 **輸入或輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [Excel 來源編輯器]  對話方塊的 [連線管理員]  節點中所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題：** [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定截斷發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 檢視錯誤的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)  
 [Excel 來源](../../integration-services/data-flow/excel-source.md)   
[Excel 連線管理員](../connection-manager/excel-connection-manager.md)
