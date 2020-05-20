---
title: 選取來源資料表和檢視 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3d3019419538c05efc28ceabc5324d373500f65c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71285139"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>選取來源資料表和檢視 (SQL Server 匯入和匯出精靈)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  指定要複製整個資料表或提供查詢之後，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [選取來源資料表和檢視表]  。 在此頁面上，您可以選取想要複製的現有資料表和檢視。 接著，將來源資料表對應到新的或現有目的資料表。 您也可以選擇檢閱個別資料行的對應，以及預覽範例資料。

> [!TIP]
> 如果您必須複製多個 SQL Server 資料庫，或資料表和檢視以外的 SQL Server 資料庫物件，請使用 [複製資料庫精靈]，而非 [匯入和匯出精靈]。 如需詳細資訊，請參閱 [使用複製資料庫精靈](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>螢幕擷取畫面 - 如果您即將複製資料表  
 下列螢幕擷取畫面顯示在您事先選取 [指定資料表複製或查詢] 頁面上的 [從一或多個資料表或檢視表複製資料] 選項時，精靈的 [選取來源資料表和檢視] 頁面範例。 在清單中，您會看到資料來源中所有可用的資料表和檢視表。
 
在此範例中，[來源]  清單包含 AdventureWorks 範例資料庫中的所有資料表。 選取的資料列顯示使用者想要將 **Sales.Customer** 資料表從來源複製至目的地的新 **Sales.CustomerNew** 資料表。 
   
 ![[匯入和匯出精靈] 的 [選取資料表] 頁面](../../integration-services/import-export-data/media/select-tables1.png "[匯入和匯出精靈] 的 [選取資料表] 頁面")
  
## <a name="screen-shot---if-you-provided-a-query"></a>螢幕擷取畫面 - 如果您已提供查詢  
 下列螢幕擷取畫面顯示在您事先選取 [指定資料表複製或查詢] 頁面上的 [寫入查詢來指定要傳送的資料] 選項時，精靈的 [選取來源資料表和檢視] 頁面範例。 [來源]  清單只會包含單一資料列，其中名為 `[Query]` 的項目代表您在 [提供來源查詢]  頁面上提供的查詢。
 
在此範例中，使用者想要將查詢結果從來源複製至目的地的 **Sales.CustomerNew** 資料表。  
    
 ![[匯入和匯出精靈] 的 [選取資料表] 頁面](../../integration-services/import-export-data/media/select-tables2.png "[匯入和匯出精靈] 的 [選取資料表] 頁面")  

## <a name="select-source-and-destination-tables"></a>選取來源和目的地資料表 
**Source**  
使用這些核取方塊，從可用的資料表和檢視清單中選取要複製到目的地的項目。 根據預設，資料來源中的資料會在未經變更的狀態下複製。 如果您建立新的目的地資料表，則也會複製新資料表的結構描述 (即，資料行和其屬性的清單)，而不需要來自資料來源的變更。

如果您已提供查詢，則清單只會包含一個名稱為 `[Query]` 的項目。 

**目的地**  
 從每個來源資料表或查詢清單中選取目的地資料表，或輸入您要精靈建立之新資料表的名稱。 如果您選取現有的目的地資料表，則資料表必須具有與來源資料表相容資料類型的資料行。  

> [!NOTE]
> 如果此時在精靈中暫停，使用外部工具 (例如  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 在目的地資料庫中手動建立新資料表，則不能立刻在可用目的地資料表清單中看到新的資料表。 若要重新整理目的地資料表清單，請退回 [選擇目的地]  頁面，並重新選取目的地資料庫來重新整理可用的資料表和檢視清單，然後再次前進到 [選取來源資料表和檢視]  。  

## <a name="optionally-review-column-mappings-and-preview-data"></a>您可以選擇檢查資料行對應及預覽資料
**編輯對應**   
選擇性地按一下 [編輯對應]  ，顯示所選取資料表的 [資料行對應]  對話方塊。 使用 [資料行對應]  對話方塊即可執行下列動作：
-   檢閱個別資料行在來源與目的地之間的對應。
-   您可以針對不想要複製的資料行選取 [忽略]  ，只複製資料行的子集。

如需詳細資訊，請參閱 [資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**預覽**  
在 [預覽資料] 對話方塊中，選擇性地按一下 [預覽] 預覽最多 200 個取樣資料列。 這會確認精靈即將複製您想要複製的資料。 如需詳細資訊，請參閱 [預覽資料](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
在您預覽資料之後，可能會想要變更已在精靈的先前頁面上選取的選項。 若要執行這些變更，請返回 [選取來源資料表和檢視表]  頁面，然後按一下 [上一步]  回到可以變更選取項目的頁面。  

## <a name="select-source-and-destination-tables-for-excel"></a>選取 Excel 的來源和目的地資料表

> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。

### <a name="excel-source-tables"></a>Excel 來源資料表
Excel 資料來源的來源資料表和檢視表清單包含兩種類型的 Excel 物件。
-   **工作表**。 工作表名稱後面接著貨幣符號 ($)，例如， **'Sheet1$'** 。
-   **命名範圍。** 命名範圍 (如有)，會依名稱列出。

如果您想要從特定的未命名資料格範圍載入或載出資料，例如 **[Sheet1$A1:B4]** ，您必須撰寫查詢。 返回 [指定資料表複製或查詢]  頁面，並選取 [寫入查詢來指定要傳送的資料]  。

### <a name="excel-destination-tables"></a>Excel 目的地資料表
如果您要將資料匯出至 Excel，您可以使用下列三種方式之一來指定目的地。
-   **工作表。** 若要指定工作表，請在工作表名稱結尾加上 $ 字元，並以分隔符號括住字串，例如 **[Sheet1$]** 。
-   **命名範圍。** 若要指定命名範圍，請只使用範圍名稱，例如 **MyDataRange**。
-   **未命名範圍。** 若要指定尚未命名的儲存格範圍，請在工作表名稱結尾加上 $ 字元、指定範圍，再以分隔符號括住字串，例如 **[Sheet1$A1:B4]** 。

> [!TIP]
> 當您使用 Excel 作為來源或目的地時，可以按一下 [編輯對應]  ，並在 [資料行對應]  頁面上檢閱資料類型對應。 

## <a name="whats-next"></a>下一步  
 選取現有的資料表和檢視進行複製並將它們對應至其目的地之後，下一頁是 [儲存並執行套件]  。 在此頁面上，您可以指定是否要立即執行複製作業。 根據組態，您也可以儲存精靈所建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件，以便在稍後進行自訂並重複使用。 如需詳細資訊，請參閱 [儲存和執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。
 
 ## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)



