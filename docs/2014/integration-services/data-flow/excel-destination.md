---
title: Excel 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldest.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84647752eb549bd5d3607637d679e58356597a6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827221"
---
# <a name="excel-destination"></a>Excel 目的地
  Excel 目的地會將資料載入至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿中的工作表或範圍。  
  
## <a name="access-modes"></a>存取模式  
 Excel 目的地提供三種不同的資料存取模式用於載入資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
> [!IMPORTANT]  
>  在 Excel 中，工作表或範圍相當於資料表或檢視。 「Excel 來源」及「Excel 目的地」編輯器中的可用資料表清單，僅會顯示現有工作表 (以附加到工作表名稱的 $ 符號識別，例如 Sheet1$) 及具名範圍 (以沒有 $ 符號的方式識別，例如 MyRange)。  
  
## <a name="usage-considerations"></a>使用狀況的考量  
 Excel 連線管理員會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支援的 Excel ISAM (Indexed Sequential Access Method，索引循序存取方法) 驅動程式，連接和讀寫資料至 Excel 資料來源。  
  
 許多現有的「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫」文件都有記錄此提供者和驅動程式的行為，而即使這些文件並非 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前置的「資料轉換服務」專用，您仍會想了解可能導致未預期結果的特定行為。 如需一般的使用和 Excel 驅動程式行為的詳細資訊，請參閱[做法：使用 ADO 與 Excel 資料，從 Visual Basic 或 VBA](https://support.microsoft.com/kb/257819)。  
  
 在將資料儲存至 Excel 目的地時，下列隨附於 Excel 驅動程式之 Jet 提供者的行為可能會導致非預期的結果。  
  
-   **儲存文字資料**。 將文字資料值儲存至 Excel 目的地時，Excel 驅動程式會在每個資料格的文字前面加上單引號字元 (')，以確保儲存的值會被解譯為文字值。 如果您擁有或開發讀取或處理儲存值的其他應用程式，您可能必須包含加在每個文字值前面的單引號字元的特殊處理。  
  
     如需如何避免包含單引號的資訊，請參閱 msdn.com 上的此篇部落格文章 [使用 SSIS 封裝中 Excel 資料流程目的地元件將資料轉換至 Excel 時，附加至所有字串的單引號](https://go.microsoft.com/fwlink/?LinkId=400876)(英文)。  
  
-   **正在儲存備忘 (ntext) 資料**。 在 Excel 資料行中成功儲存長於 255 個字元的字串之前，驅動程式必須能將目的地資料行的資料類型辨識為 **備忘** ，而不是 **字串**。 如果目的地資料表已包含資料列，則驅動程式所取樣的前幾個資料列必須在備忘資料行中至少包含一個值長於 255 個字元的執行個體。 如果在套件設計期間或在執行階段建立目的地資料表，則 CREATE TABLE 陳述式必須使用 LONGTEXT （或其同義字之一） 作為備忘資料行的資料類型。  
  
-   **資料類型**。 Excel 驅動程式只能辨識有限的一組資料類型。 例如，所有的數值資料行都會被解譯為倍整數 (DT_R8)，而所有的字串資料行 (備忘錄資料行除外) 全都會被解譯成 255 個字元的 Unicode 字串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 對應 Excel 資料類型的情況如下：  
  
    -   數值 - 雙精確度浮點數 (DT_R8)  
  
    -   貨幣 - 貨幣 (DT_CY)  
  
    -   布林值 - 布林值 (DT_BOOL)  
  
    -   日期/時間`datetime`(DT_DATE)  
  
    -   字串 - Unicode 字串，長度 255 (DT_WSTR)  
  
    -   備忘錄 - Unicode 文字資料流 (DT_NTEXT)  
  
-   **資料類型和長度轉換**： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不會隱含地轉換資料類型。 因此，您可能必須使用衍生的資料行轉換或資料轉換，在將 Excel 資料載入到非 Excel 目的地之前明確轉換 Excel 資料，或是在將非 Excel 資料載入到 Excel 目的地之前轉換資料。 在這種情況下，使用「匯入和匯出精靈」建立初始封裝可能很有用，因為這個精靈會為您設定必要的轉換。 某些轉換範例可能必須包含下列各項：  
  
    -   Unicode Excel 字串資料行與具有特定字碼頁之非 Unicode 字串資料行之間的轉換。  
  
    -   255 個字元之 Excel 字串資料行與不同長度之字串資料行之間的轉換。  
  
    -   雙精確度 Excel 數值資料行與其他類型之數值資料行之間的轉換。  
  
## <a name="configuration-of-the-excel-destination"></a>設定 Excel 目的地  
 Excel 目的地會使用 Excel 連接管理員，以連接到資料來源，而連接管理員會指定要使用的活頁簿檔案。 如需詳細資訊，請參閱 [Excel Connection Manager](../connection-manager/excel-connection-manager.md)。  
  
 Excel 目的地擁有一個規則輸入與一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關 **[Excel 目的地編輯器]** 對話方塊中可設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Excel 目的地編輯器 &#40;連線管理員頁面&#41;](../excel-destination-editor-connection-manager-page.md)  
  
-   [Excel 目的地編輯器 &#40;對應頁面&#41;](../excel-destination-editor-mappings-page.md)  
  
-   [Excel 目的地編輯器 &#40;錯誤輸出頁面&#41;](../excel-destination-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之所有屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [Excel 自訂屬性](excel-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 SQL Server Integration Services (SSIS) 從 Excel 匯入資料，或將資料匯出至 Excel](../load-data-to-from-excel-with-ssis.md)  
  
-   [使用 Foreach 迴圈容器來執行 Excel 檔案和資料表迴圈](../control-flow/foreach-loop-container.md)  
  
-   [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
  
-   部落格文章[Integration Services 中的 Excel、 3 的第 1 部分：連接與元件](https://go.microsoft.com/fwlink/?LinkId=217674)，位於 dougbert.com  
  
-   部落格文章[Integration Services 中的 Excel、 3 第 2 部分：資料表和資料型別](https://go.microsoft.com/fwlink/?LinkId=217675)，dougbert.com 上。  
  
-   部落格文章[Integration Services 中的 Excel、 3 第 3 部分：問題與替代方案](https://go.microsoft.com/fwlink/?LinkId=217676)，dougbert.com 上。  
  
## <a name="see-also"></a>另請參閱  
 [Excel 來源](excel-source.md)   
 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)   
 [資料流程](data-flow.md)   
 [以指令碼工作處理 Excel 檔案](../extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
