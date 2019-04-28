---
title: Excel 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsource.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 15ef45a4f3bfb0b74de2472a5b2f0d8e483edab1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856943"
---
# <a name="excel-source"></a>Excel 來源
  Excel 來源會從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿中的工作表或範圍擷取資料。  
  
 Excel 來源會提供四種不同的資料存取模式來擷取資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
-   儲存在變數中之 SQL 陳述式的結果。  
  
> [!IMPORTANT]  
>  在 Excel 中，工作表或範圍相當於資料表或檢視。 「Excel 來源」及「Excel 目的地」編輯器中的可用資料表清單，會顯示現有工作表 (以附加到工作表名稱的 $ 符號識別，例如 Sheet1$) 及具名範圍 (以沒有 $ 符號的方式識別，例如 MyRange)。 如需詳細資訊，請參閱＜使用狀況的考量＞一節。  
  
 Excel 來源會使用 Excel 連接管理員連接到資料來源，而連接管理員會指定要使用的活頁簿檔案。 如需詳細資訊，請參閱 [Excel Connection Manager](../connection-manager/excel-connection-manager.md)。  
  
 Excel 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="usage-considerations"></a>使用狀況的考量  
 Excel 連線管理員會使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支援的 Excel ISAM (Indexed Sequential Access Method，索引循序存取方法) 驅動程式，連接和讀寫資料至 Excel 資料來源。  
  
 許多現有的「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫」文件都有記錄此提供者和驅動程式的行為，而即使這些文件並非 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前置的「資料轉換服務」專用，您仍會想了解可能導致未預期結果的特定行為。 如需一般的使用和 Excel 驅動程式行為的詳細資訊，請參閱[做法：使用 ADO 與 Excel 資料，從 Visual Basic 或 VBA](https://support.microsoft.com/kb/257819)。  
  
 下列使用 Excel 驅動程式之 Jet 提供者的行為，在從 Excel 資料來源讀取資料時，可能導致未預期的結果。  
  
-   **資料來源**。 Excel 活頁簿中資料的來源可以是工作表 (必須附加 $ 符號，例如 Sheet1$) 或已命名的範圍 (例如 MyRange)。 在 SQL 陳述式中，工作表的名稱必須加以分隔 (例如 [Sheet1$])，以避免 $ 符號造成的語法錯誤。 「查詢產生器」會自動加入這些分隔符號。 當您指定工作表或範圍時，驅動程式會讀取連續的資料格區塊，從工作表或範圍左上角的第一個非空白資料格開始。 因此，來源資料的資料列不可以空白，或標題或標頭資料列與資料列之間不可以有空白資料列。  
  
-   **遺漏值**。 Excel 驅動程式會在指定來源中讀取特定資料列數目 (依預設為 8 個資料列)，以猜測各資料行的資料類型。 當資料行可能包含混合資料類型，尤其是數值資料與文字資料混合時，驅動程式會做出有利於大部分資料類型的決定，並於包含其他類型資料的資料格中傳回 Null 值。 (在繫結中，以數值類型優先)。Excel 工作表中大部分的資料格格式化選項，似乎都不會影響這項資料類型決定。 您可以藉由指定「匯入模式」來修改 Excel 驅動程式的這項行為。 若要指定匯入模式，請新增`IMEX=1`中的 Excel 連接管理員的連接字串中的擴充屬性值**屬性**視窗。 如需詳細資訊，請參閱[PRB:Excel 傳回的值當作 NULL 使用 DAO OpenRecordset](https://support.microsoft.com/kb/194124)。  
  
-   **截斷的文字**。 當驅動程式判斷出某個 Excel 資料行包含文字資料時，驅動程式將會根據其取樣的最長值來選取資料類型 (字串或備忘錄)。 如果驅動程式未在其取樣的資料列中發現任何長度超過 255 個字元的值，則會將該資料行視為 255 個字元字串資料行而非備忘錄資料行 因此，長度超過 255 個字元的值可能會被截斷。 若要以不截斷的方式從備忘資料行匯入資料，您必須確保至少在其中一個取樣資料列中的備忘錄資料行包含長度超過 255 個字元的值，否則您就必須增加驅動程式取樣的資料列數目，使其包含這類資料列。 您可以提高 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** 登錄機碼底下 **TypeGuessRows** 的值，藉以增加取樣的資料列數目。 如需詳細資訊，請參閱[PRB:從 Jet 4.0 OLEDB 來源的資料傳輸錯誤而失敗](https://support.microsoft.com/kb/281517)。  
  
-   **資料類型**。 Excel 驅動程式只能辨識有限的一組資料類型。 例如，所有的數值資料行都會被解譯為倍整數 (DT_R8)，而所有的字串資料行 (備忘錄資料行除外) 全都會被解譯成 255 個字元的 Unicode 字串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 對應 Excel 資料類型的情況如下：  
  
    -   數值 - 雙精確度浮點數 (DT_R8)  
  
    -   貨幣 - 貨幣 (DT_CY)  
  
    -   布林值 - 布林值 (DT_BOOL)  
  
    -   日期/時間- `datetime` (DT_DATE)  
  
    -   字串 - Unicode 字串，長度 255 (DT_WSTR)  
  
    -   備忘錄 - Unicode 文字資料流 (DT_NTEXT)  
  
-   **資料類型和長度轉換**： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不會隱含地轉換資料類型。 因此，您可能必須使用衍生的資料行轉換或資料轉換，在將 Excel 資料載入到非 Excel 目的地之前明確轉換 Excel 資料，或是在將非 Excel 資料載入到 Excel 目的地之前轉換資料。 在這種情況下，使用「匯入和匯出精靈」建立初始封裝可能很有用，因為這個精靈會為您設定必要的轉換。 某些轉換範例可能必須包含下列各項：  
  
    -   Unicode Excel 字串資料行與具有特定字碼頁之非 Unicode 字串資料行之間的轉換  
  
    -   255 個字元之 Excel 字串資料行與不同長度之字串資料行之間的轉換  
  
    -   雙精確度 Excel 數值資料行與其他類型之數值資料行之間的轉換  
  
## <a name="excel-source-configuration"></a>Excel 來源組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [Excel 來源編輯器] 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Excel 來源編輯器 &#40;連線管理員頁面&#41;](../excel-source-editor-connection-manager-page.md)  
  
-   [Excel 來源編輯器 &#40;資料行頁面&#41;](../excel-source-editor-columns-page.md)  
  
-   [Excel 來源編輯器 &#40;錯誤輸出頁面&#41;](../excel-source-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之所有屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [Excel 自訂屬性](excel-custom-properties.md)  
  
 如需循環使用 Excel 檔案群組的資訊，請參閱 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../control-flow/foreach-loop-container.md)。  
  
## <a name="related-tasks"></a>相關工作  

-   [使用 SQL Server Integration Services (SSIS) 從 Excel 匯入資料，或將資料匯出至 Excel](../load-data-to-from-excel-with-ssis.md)

-   [在資料流程元件中將查詢參數對應至變數](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [使用 Foreach 迴圈容器來執行 Excel 檔案和資料表迴圈](../control-flow/foreach-loop-container.md)  
  
## <a name="related-content"></a>相關內容  
  
-   hrvoje.piasevoli.com 上的部落格文章： [Importing data from 64-bit Excel in SSIS](https://go.microsoft.com/fwlink/?LinkId=217673)(從 SSIS 中的 64 位元 Excel 匯入資料)  
  
-   部落格文章[Integration Services 中的 Excel、 3 的第 1 部分：連接與元件](https://go.microsoft.com/fwlink/?LinkId=217674)，位於 dougbert.com  
  
-   部落格文章[Integration Services 中的 Excel、 3 第 2 部分：資料表和資料型別](https://go.microsoft.com/fwlink/?LinkId=217675)，dougbert.com 上。  
  
-   部落格文章[Integration Services 中的 Excel、 3 第 3 部分：問題與替代方案](https://go.microsoft.com/fwlink/?LinkId=217676)，dougbert.com 上。  
  
-   部落格文章[連接到 Excel (XLSX) 在 SSIS 中](https://microsoft-ssis.blogspot.com/2014/02/connecting-to-excel-xlsx-in-ssis.html)。  
  
  
