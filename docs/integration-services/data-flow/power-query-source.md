---
title: Power Query 來源 | Microsoft Docs
description: 了解如何在 SQL Server Integration Services 資料流程中設定 Power Query 來源
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: integration-services
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.powerqueryconnmgr.f1
- sql13.ssis.designer.powerquerysource.queries.f1
- sql13.ssis.designer.powerquerysource.connmgrs.f1
- sql14.ssis.designer.powerqueryconnmgr.f1
- sql14.ssis.designer.powerquerysource.queries.f1
- sql14.ssis.designer.powerquerysource.connmgrs.f1
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
manager: craigg
ms.openlocfilehash: 3ca141c40420b4d2e71a660220075413d9ca8c64
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66015075"
---
# <a name="power-query-source-preview"></a>Power Query 來源 (預覽)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



本文說明如何在 SQL Server Integration Services (SSIS) 資料流程中設定 Power Query 來源的屬性。 Power Query 是一種技術，可讓您使用 Excel/Power BI Desktop 連線到各種資料來源並轉換資料。 如需詳細資訊，請參閱 [Power Query - 概觀與學習](https://support.office.com/article/power-query-overview-and-learning-ed614c81-4b00-4291-bd3a-55d80767f81d) \(機器翻譯\) 一文。 Power Query 所產生的指令碼可以複製並貼到 SSIS 資料流程中的 Power Query 來源並加以設定。
  
> [!NOTE]
> 針對目前的預覽版本，為了方便進行快速收集意見反應且頻繁地增強功能，Power Query 來源只能在 SQL Server Data Tools (SSDT) 和 Azure Data Factory (ADF) 的 Azure SSIS Integration Runtime (IR) 中使用。 您可以從[此處](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017)下載支援 Power Query 來源的最新 SSDT。 若要佈建 Azure-SSIS IR，請參閱[在 ADF 中佈建 SSIS](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure) 一文。

## <a name="configure-the-power-query-source"></a>設定 Power Query 來源

若要在 SSDT 中開啟 [Power Query 來源編輯器]，將 [Power Query 來源] 從 SSIS 工具箱拖放到資料流程設計工具，並在其上按兩下。  

![PQ 來源](media/power-query-source/pq-source.png)

隨即會在左側顯示三個索引標籤。 在 [查詢] 索引標籤上，您可以從下拉式功能表中選取查詢模式。
-   [單一查詢] 模式可讓您從 Excel/Power BI Desktop 複製並貼上單一 Power Query 指令碼。
-   [來自變數的單一查詢] 模式可讓您指定包含要執行之查詢的字串變數。

![PQ 來源 [查詢] 索引標籤單一](media/power-query-source/pq-source-queries-tab-single.png)

在 [連線管理員] 索引標籤上，您可以新增或移除包含資料來源存取認證的 Power Query 連線管理員。 選取 [偵測資料來源] 按鈕會識別查詢中參考的資料來源並列出它們，以指派適當的現有 Power Query 連線管理員或建立新的。

![PQ 來源 [連線管理員] 索引標籤偵測](media/power-query-source/pq-source-connection-managers-tab-detect.png)

![PQ 來源 [連線管理員] 索引標籤新增](media/power-query-source/pq-source-connection-managers-tab-add.png)

最後，在 [資料行] 索引標籤上，您可以編輯輸出資料行資訊。

![PQ 來源 [資料行] 索引標籤](media/power-query-source/pq-source-columns-tab.png)

## <a name="configure-the-power-query-connection-manager"></a>設定 Power Query 連線管理員

在 SSDT 上使用 Power Query 來源設計資料流程時，您可以透過下列方式來建立新的 Power Query 連線管理員：
- 在選取 [新增]/[偵測資料來源] 按鈕，然後從下拉式功能表中選取 [<New connection...>] 之後 (如上所述)，間接在 Power Query 來源的 [連線管理員] 索引標籤上建立它。
- 以滑鼠右鍵按一下封裝的 [連線管理員] 面板，然後從下拉式功能表中選取 [新增連線...]。

![PQ 來源 [連線管理員] 面板新增](media/power-query-source/pq-source-connection-managers-panel-add.png)

在 [加入 SSIS 連線管理員] 對話方塊中，從連線管理員類型清單中按兩下 [PowerQuery]。

![PQ 來源 [連線管理員] 面板新增對話方塊](media/power-query-source/pq-source-connection-managers-panel-add-dialog.png)

在 [Power Query 連線管理員編輯器] 中，您必須指定**資料來源種類**、**資料來源路徑**和**驗證種類**，以及指派適當的存取認證。 對於**資料來源種類**，您可以從下拉式功能表中目前的 22 個種類內選取其中一個。

![PQ 來源 [連線管理員編輯器] 種類](media/power-query-source/pq-source-connection-manager-editor-kind.png)

在這些來源 (**Oracle**、**DB2**、**MySQL**、**PostgreSQL**、**Teradata**、**Sybase**) 中，有一些需要額外安裝可從 [Power Query 必要條件](https://support.office.com/article/data-source-prerequisites-power-query-6062cf52-c764-45d0-a1c6-fbf8fc05b05a) \(機器翻譯\) 一文取得的 ADO.NET 驅動程式。 您可以使用自訂安裝介面，在 Azure-SSIS IR 上安裝它們，請參閱[自訂 Azure-SSIS IR](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) 一文。

對於**資料來源路徑**，您可以輸入不需驗證資訊，即可組成連接字串的資料來源特有屬性。 例如，適用於 **SQL** 資料來源的路徑格式為 `<Server>;<Database>`。 您可以選取 [編輯] 按鈕，以將值指派給組成路徑的資料來源特有屬性。

![PQ 來源 [連線管理員編輯器] 路徑](media/power-query-source/pq-source-connection-manager-editor-path.png)

最後，對於**驗證種類**，您可以從下拉式功能表中選取 [匿名]/[Windows 驗證]/[使用者名稱密碼]/[金鑰]、輸入適當的存取認證，然後選取 [測試連接] 按鈕，以確保 Power Query 來源已正確設定。

![PQ 來源 [連線管理員編輯器] 驗證](media/power-query-source/pq-source-connection-manager-editor-authentication.png)

### <a name="current-limitations"></a>目前的限制

-   目前無法使用 **Oracle** 資料來源，因為 Oracle ADO.NET 驅動程式無法安裝於 Azure-SSIS IR；因此，暫時請改安裝 Oracle ODBC 驅動程式，並使用 **ODBC** 資料來源連線到 Oracle，請參閱[自訂 AZURE-SSIS IR](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) 一文中的 **ORACLE 標準 ODBC** 範例。

-   目前無法以自訂安裝的狀態在 Azure-SSIS IR 上使用 **Web** 資料來源，所以暫時請以無自訂安裝的狀態在 Azure-SSIS IR 上使用它。

## <a name="next-steps"></a>後續步驟
了解如何在 Azure-SSIS IR 中執行 SSIS 封裝以作為 ADF 管線中的第一級活動。 請參閱[執行 SSIS 封裝活動執行階段](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)一文。
