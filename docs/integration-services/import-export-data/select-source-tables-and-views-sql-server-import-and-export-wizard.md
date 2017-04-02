---
title: "選取來源資料表和檢視 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.selectsourcetablesandviews.f1"
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 96
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 88
---
# 選取來源資料表和檢視 (SQL Server 匯入和匯出精靈)
  指定要複製整個資料表或提供查詢之後，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [選取來源資料表和檢視表]。 在此頁面上，您可以選取想要複製的現有資料表和檢視。 接著，將來源資料表對應到新的或現有目的資料表。 您也可以選擇檢閱個別資料行的對應，以及預覽範例資料。

> [!TIP] 如果您必須複製多個資料庫，或資料表和檢視以外的資料庫物件，請使用 [複製資料庫精靈]，而非 [匯入和匯出精靈]。 如需詳細資訊，請參閱[使用複製資料庫精靈](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="screen-shot---what-you-see-if-youre-going-to-copy-tables"></a>螢幕擷取畫面 - 複製資料表時將看到的畫面  
 下列螢幕擷取畫面顯示在您事先選取 [指定資料表複製或查詢] 頁面上的 [從一個或多個資料表或檢視表複製資料] 選項時，精靈的 [選取來源資料表和檢視] 頁面。 在清單中，您會看到資料來源中所有可用的資料表和檢視表。
 
在本例中，使用者想要將 **Sales.Customer** 資料表從來源複製至目的地的新 **Sales.CustomerNew** 資料表。 
   
 ![Select tables page of the Import and Export Wizard](../../integration-services/import-export-data/media/select-tables1.png "Select tables page of the Import and Export Wizard")
  
## <a name="screen-shot---what-you-see-if-you-provided-a-query"></a>螢幕擷取畫面 - 提供查詢時將看到的畫面  
 下列螢幕擷取畫面顯示在您事先選取 [指定資料表複製或查詢] 頁面上的 [寫入查詢來指定要傳送的資料] 選項，並在 [提供來源查詢] 頁面提供查詢時，精靈的 [選取來源資料表和檢視表] 頁面。 在清單中，您只會看到單一資料列，其中，Source 資料行中的項目代表您提供的查詢。
 
在此範例中，使用者想要將查詢結果從來源複製至目的地的 **Sales.CustomerNew** 資料表。  
    
 ![Select tables page of the Import and Export Wizard](../../integration-services/import-export-data/media/select-tables2.png "Select tables page of the Import and Export Wizard")  

## <a name="select-source-and-destination-tables"></a>選取來源和目的地資料表 
**來源**  
使用這些核取方塊，從可用的資料表和檢視清單中選取要複製到目的地的項目。 根據預設，資料來源中的資料會在未經變更的狀態下複製。 如果您建立新的目的資料表，結構描述也會從資料來源以未經變更的狀態複製。

如果您提供查詢，清單只會包含一個名稱為 \[Query\] 的項目。 

**目的地**  
 從每個來源資料表或查詢清單中選取目的地資料表，或輸入您要精靈建立之新資料表的名稱。 如果您選取現有的目的地資料表，則資料表必須具有與來源資料表相容資料類型的資料行。  

> [!NOTE] 如果此時在精靈中暫停，使用外部工具 (例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 在目的地資料庫中手動建立新資料表，則不能立刻在可用目的地資料表清單中看到新的資料表。 若要重新整理目的地資料表清單，請退回 [選擇目的地] 頁面，並重新選取目的地資料庫來重新整理可用的資料表和檢視清單，然後再次前進到 [選取來源資料表和檢視]。  

## <a name="select-source-and-destination-tables-for-excel"></a>選取 Excel 的來源和目的地資料表

### <a name="excel-source-tables"></a>Excel 來源資料表
Excel 資料來源的來源資料表和檢視表清單包含兩種類型的 Excel 物件。
-   **工作表**。 工作表名稱後面接著貨幣符號 ($)，例如，**'Sheet1$'**。
-   **命名範圍。** 命名範圍 (如有)，會依名稱列出。

如果您想要從特定的未命名資料格範圍載入或載出資料，例如 **[Sheet1$A1:B4]**，您必須撰寫查詢。 返回 [指定資料表複製或查詢] 頁面，並選取 [寫入查詢來指定要傳送的資料]。

無論是指定工作表或範圍為來源資料表，驅動程式會讀取「連續的」資料格區塊，從工作表或範圍左上角的第一個非空白資料格開始。 結果就是來源資料中不能有空白的資料列。 例如，資料行標頭和資料列之間不能有空白的資料列。 如果工作表頂端在資料上方有某個標題後面有空白的資料列，您就無法查詢工作表。 在 Excel 中，您必須將名稱指派給資料範圍，查詢命名範圍，而不是工作表。

### <a name="excel-destination-tables"></a>Excel 目的地資料表
如果您要將資料匯出至 Excel，您可以使用下列三種方式之一來指定目的地。
-   **工作表。** 若要指定工作表，請在工作表名稱結尾加上 $ 字元，並以分隔符號括住字串，例如 **[Sheet1$]**。
-   **命名範圍。** 若要指定命名範圍，請只使用範圍名稱，例如 **MyDataRange**。
-   **未命名範圍。** 若要指定尚未命名的儲存格範圍，請在工作表名稱結尾加上 $ 字元、指定範圍，再以分隔符號括住字串，例如 **[Sheet1$A1:B4]**。

## <a name="special-considerations-for-excel-sources-and-destinations"></a>Excel 來源和目的地的特殊考量
當您使用 Excel 作為來源或目的地時，可以按一下 [編輯對應]，並在 [資料行對應] 頁面上檢閱資料類型對應。 

**Excel 活頁簿中的資料類型**。 Excel 不是一般的資料庫。 其資料行沒有固定的資料類型。 精靈只會辨識有限的 Excel 資料類型集合：數字、貨幣、布林值，日期/時間、字串 (255 個或更少的字元) 以及註解 (255 個以上字元)。 精靈會在 Excel 資料來源中讀取特定資料列數目 (依預設為 8 個資料列)，以猜測各資料行的資料類型。

當精靈必須執行明確的資料類型轉換以從 Excel 載入或載出資料時，通常會顯示 [檢閱資料類型對應] 頁面，在此可以檢閱這些轉換。 這些轉換可能包括下列項目。
-   雙精確度 Excel 數值資料行與其他類型之數值資料行之間的轉換。
-   Unicode Excel 字串資料行與具有特定字碼頁之非 Unicode 字串資料行之間的轉換。
-   255 個字元之 Excel 字串資料行與不同長度之字串資料行之間的轉換。

### <a name="special-considerations-for-excel-sources"></a>Excel 來源的特殊考量
**匯入的資料中有 Null 或遺漏值**。 當由精靈所取樣的前八個資料列中，Excel 資料行似乎包含混合的資料類型時，例如混合使用數值和文字值，精靈會挑選多數的資料類型作為該資料行的資料類型，而包含其他類型資料的資料格則傳回 Null 值。 沒有任何方法可以變更精靈的此種行為。

**匯入的資料中有截斷的字串**。 當精靈判斷出某個 Excel 資料行包含文字資料時，精靈將會根據其前八個資料列取樣的最長值，來挑選字串或備忘的資料行資料類型。 如果精靈未在其取樣的資料列中發現任何長度超過 255 個字元的值，則會將該資料行視為 255 個字元的字串資料行，而非備忘資料行，並截斷超過 255 個字元的值。 若要從備忘資料行中匯入資料卻不截斷，您必須確保備忘資料行在前八個資料列中，至少包含一個超過 255 個字元的值。

### <a name="special-considerations-for-excel-destinations"></a>Excel 目的地的特殊考量
**指定現有的範圍**。 如果範圍的寬度不夠，也就是說，資料行數比來源資料少，當您將現有的範圍指定為目的地時，就會發生錯誤。 不過，如果您指定的範圍不夠長，也就是說，資料列數比來源資料少，精靈會繼續寫入資料列並延伸範圍定義，使符合新的資料列數目。

**正在儲存備忘 (ntext) 資料**。 在 Excel 資料行中成功儲存長於 255 個字元的字串之前，精靈必須能將目的地資料行的資料類型辨識為**備忘**，而不是**字串**。
-   如果目的地資料表已包含資料列，則精靈取樣的前八資料列必須在備忘資料行中至少包含一個值超過 255 個字元的資料列。
-   如果目的地資料表是由精靈建立，則 **CREATE TABLE** 陳述式必須使用 **LONGTEXT** (或其同義字之一) 作為備忘資料行的資料類型。 按一下 [資料行對應] 頁面上 [建立目的地資料表] 選項旁的 [編輯 SQL]，修訂 **CREATE TABLE** 陳述式。

## <a name="optionally-edit-column-mappings-and-preview-sample-data"></a>選擇性編輯資料行的對應及預覽取樣資料
**編輯對應**   
選擇性地按一下 [編輯對應]，顯示所選取資料表的 [資料行對應] 對話方塊。 使用 [資料行對應] 對話方塊即可執行下列動作：
-   檢閱個別資料行在來源與目的地之間的對應。
-   您可以針對不想要複製的資料行選取 [忽略]，只複製資料行的子集。

如需詳細資訊，請參閱[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。  

**預覽**  
在 [預覽資料] 對話方塊中，選擇性地按一下 [預覽] 預覽最多 200 個取樣資料列。 這會確認精靈即將複製您想要複製的資料。 如需詳細資訊，請參閱[預覽資料](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。  
  
在您預覽資料之後，可能會想要變更已在精靈的先前頁面上選取的選項。 若要執行這些變更，請返回 [選取來源資料表和檢視表] 頁面，然後按一下 [上一步] 回到可以變更選取項目的頁面。  

## <a name="whats-next"></a>下一步  
 選取現有的資料表和檢視進行複製並將它們對應至其目的地之後，下一頁是 [儲存並執行套件]。 在此頁面上，您可以指定是否要立即執行複製作業。 根據組態，您也可以儲存精靈所建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，以便在稍後進行自訂並重複使用。 如需詳細資訊，請參閱[儲存和執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  
