---
title: OLE DB 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a81d65cfd0716ba386db98b3d9973fb4e57876a7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298182"
---
# <a name="ole-db-destination"></a>OLE DB 目的地

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 目的地會使用資料庫的資料表、檢視或 SQL 命令將資料載入各種符合 OLE DB 標準的資料庫。 例如，OLE DB 來源可以將資料載入至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料表中。  
  
> [!NOTE]  
>  如果資料來源為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，則資料來源需要舊版 Excel 以外的連接管理員。 如需詳細資訊，請參閱 [連接至 Excel 活頁簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
  
 OLE DB 目的地提供用於載入資料的五種不同資料存取模式：  
  
-   資料表或檢視。 您可以指定現有的資料表或檢視，或者建立新資料表。  
  
-   使用快速載入選項的資料表或檢視。 您可以指定現有的資料表，也可以新建資料表。  
  
-   在變數中指定的資料表或檢視。  
  
-   在變數中指定之使用快速載入選項的資料表或檢視。  
  
-   SQL 陳述式的結果。  
  
> [!NOTE]  
>  OLE DB 目的地不支援參數。 如果需要執行參數化 INSERT 陳述式，請考慮 OLE DB 命令轉換。 如需相關資訊，請參閱 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)。  
  
 當 OLE DB 目的地載入使用雙位元組字元集 (DBCS) 的資料時，如果資料存取模式未使用快速載入選項，而 OLE DB 連接管理員使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB)，則資料可能會損毀。 若要確定 DBCS 資料的完整性，您應該將 OLE DB 連線管理員設定為使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，或使用下列其中一個快速載入存取模式：[資料表或檢視表 - 快速載入]  或 [資料表名稱或檢視表名稱變數 - 快速載入]  。 兩個選項都可從 [OLE DB 目的地編輯器]  對話方塊使用。 程式設計 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 物件模型時，您應該將 AccessMode 屬性設為 [使用 FastLoad 的 OpenRowset]  ，或 [從變數使用 FastLoad OpenRowset]  。  
  
> [!NOTE]  
>  如果使用「[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中的 [OLE DB 目的地編輯器]  對話方塊來建立 OLE DB 目的地插入資料的目的地資料表，則您可能必須手動選取新建立的資料表。 當 OLE DB 提供者 (例如 DB2 的 OLE DB 提供者) 自動將結構描述識別碼加入資料表名稱時，需進行手動選取。  
  
> [!NOTE]  
>  視目的地類型而定，[OLE DB 目的地編輯器]  對話方塊產生的 CREATE TABLE 陳述式可能需要進行修改。 例如，某些目的地並不支援 CREATE TABLE 陳述式所使用的資料類型。  
  
 此目的地使用 OLE DB 連接管理員連接到資料來源，且連接管理員會指定要使用的 OLE DB 提供者。 如需相關資訊，請參閱 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案亦提供您建立 OLE DB 連線管理員所在的資料來源物件，讓 OLE DB 目的地使用資料來源和資料來源檢視。  
  
 OLE DB 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不一定要將輸入資料行對應到所有目的地資料行，但因目的地資料行屬性的不同，如果輸入資料行未對應到目的地資料行，則可能發生錯誤。 例如，如果目的地資料行不允許 Null 值，則輸入資料行必須對應到該資料行。 此外，對應之資料行的資料類型必須相容。 例如，您不能將字串資料類型的輸入資料行對應到數值資料類型的目的地資料行。  
  
 OLE DB 目的地具有一個規則輸入和一個錯誤輸出。  
  
 如需有關資料類型的詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## <a name="fast-load-options"></a>快速載入選項  
 如果 OLE DB 目的地使用快速載入資料存取模式，則您可以在 **OLE DB 目的地編輯器**這個使用者介面中為目的地指定下列快速載入選項：  
  
-   保留匯入資料檔中的識別值或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指派的唯一值。  
  
-   大量載入作業期間保留 Null 值。  
  
-   大量匯入作業期間檢查目標資料表或檢視的條件約束。  
  
-   大量載入作業期間需要資料表層級鎖定。  
  
-   指定批次中的資料列數目以及認可大小。  
  
 部分快速載入選項儲存在 OLE DB 目的地的特定屬性中。 例如，FastLoadKeepIdentity 指定是否要保留識別值、FastLoadKeepNulls 指定是否要保留 Null 值，而 FastLoadMaxInsertCommitSize 則指定要認可為批次的資料列數目。 其他快速載入選項儲存在 FastLoadOptions 屬性的逗號分隔清單中。 如果 OLE DB 目的地使用儲存在 FastLoadOptions 及列在 [OLE DB 目的地編輯器]  對話方塊中的所有快速載入選項，屬性的值便會設定為 **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**。 1000 值代表目的地設定為使用 1000 列的批次。  
  
> [!NOTE]  
>  目的地的任何條件約束失敗都會使 FastLoadMaxInsertCommitSize 所定義的整個資料列批次失敗。  
  
 除了 [OLE DB 目的地編輯器]  對話方塊中公開的快速載入選項以外，您還可以在 [進階編輯器]  對話方塊的 FastLoadOptions 屬性中輸入選項，將 OLE DB 目的地設定為使用下列大量載入選項。  
  
|快速載入選項|描述|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|指定要插入的大小 (以 KB 為單位)。 選項的格式為 **KILOBYTES_PER_BATCH** = \<正整數值 **>** 。|  
|FIRE_TRIGGERS|指定是否要針對插入資料表上引發觸發程序。 選項的格式為 **FIRE_TRIGGERS**。 選項的存在代表觸發程序會引發。|  
|ORDER|指定如何儲存輸入資料。 選項的格式為 ORDER \<資料行名稱> ASC&#124;DESC。 可以列出任何數目的資料行，也可以選擇包含排序順序。 如果省略排序順序，大量插入作業會假設資料沒有排序。<br /><br /> 注意:如果您使用 ORDER 選項依照資料表的叢集索引來排序輸入資料，將可改善效能。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 關鍵字通常是以大寫字母輸入，但是這些關鍵字並不區分大小寫。  
  
 若要深入了解有關快速載入選項的詳細資訊，請參閱 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
## <a name="troubleshooting-the-ole-db-destination"></a>疑難排解 OLE DB 目的地  
 您可以記錄 OLE DB 目的地對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，針對 OLE DB 目的地所執行的將資料儲存至外部資料來源的作業進行疑難排解。 若要記錄 OLE DB 目的地對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷]  事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-destination"></a>設定 OLE DB 目的地  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB 自訂屬性](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用 OLE DB 目的地來載入資料](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>OLE DB 目的地編輯器 (連接管理員頁面)
  使用 **[OLE DB 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面來選取目的地的 OLE DB 連接。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
> [!NOTE]  
>  如果資料來源為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，則資料來源需要舊版 Excel 以外的連接管理員。 如需詳細資訊，請參閱 [連接至 Excel 活頁簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
  
> [!NOTE]  
>  在 **[OLE DB 目的地編輯器]** 中無法使用 OLE DB 目的地的 **CommandTimeout**屬性，但可使用 **[進階編輯器]** 來設定這個屬性。 此外， **[進階編輯器]** 中只會有特定的快速載入選項。 如需有關這些屬性的詳細資訊，請參閱＜ [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)＞的＜OLE DB 目的地＞一節。  
  
### <a name="static-options"></a>靜態選項  
 **[無快取]**  
 從清單中選取現有的連線管理員，或按一下 [新增]  來建立新的連線。  
  
 **新增**  
 使用 [設定 OLE DB 連線管理員]  對話方塊建立新的連線管理員。  
  
 **資料存取模式**  
 指定將資料載入目的地的方法。 請注意，雙位元組字集 (DBCS) 資料需要使用其中一種快速載入選項。 如需有關快速載入資料存取模式 (已針對大量插入進行過最佳化) 的詳細資訊，請參閱＜ [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)＞。  
  
|選項|描述|  
|------------|-----------------|  
|資料表或檢視|將資料載入 OLE DB 目的地中的資料表或檢視。|  
|資料表或檢視 - 快速載入|將資料載入 OLE DB 目的地中的資料表或檢視，並使用快速載入選項。 如需有關快速載入資料存取模式 (已針對大量插入進行過最佳化) 的詳細資訊，請參閱＜ [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)＞。|  
|資料表名稱或檢視名稱變數|請在變數中指定資料表或檢視名稱。<br /><br /> **相關資訊**：[在套件中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|資料表名稱或檢視名稱變數 - 快速載入|在變數中指定資料表或檢視名稱，並使用快速載入選項來載入資料。 如需有關快速載入資料存取模式 (已針對大量插入進行過最佳化) 的詳細資訊，請參閱＜ [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)＞。|  
|SQL (命令)|使用 SQL 查詢，將資料載入到 OLE DB 目的地。|  
  
 **預覽**  
 使用 [預覽查詢結果]  對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
### <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
 **[資料存取模式]** 的每個設定都會顯示該設定專用的動態選項集。 下列章節將一一描述每個 **[資料存取模式]** 設定可用的動態選項。  
  
#### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **資料表或檢視的名稱**  
 從資料來源中可用的清單中選取資料表或檢視名稱。  
  
 **新增**  
 使用 [建立資料表]  對話方塊建立新的資料表。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
#### <a name="data-access-mode--table-or-view---fast-load"></a>資料存取模式 = 資料表或檢視 - 快速載入  
 **資料表或檢視的名稱**  
 使用此清單從資料庫選取資料表或檢視，或按一下 [新增]  建立新的資料表。  
  
 **新增**  
 使用 [建立資料表]  對話方塊建立新的資料表。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **保留識別**  
 指定載入資料時是否複製識別值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 **false**。  
  
 **保留 Null**  
 指定載入資料時是否複製 Null 值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 **false**。  
  
 **資料表鎖定**  
 指定載入期間是否鎖定資料表。 此屬性的預設值為 **true**。  
  
 **檢查條件約束**  
 指定目的地在載入資料時是否檢查條件約束。 此屬性的預設值為 **true**。  
  
 **每批次的資料列**  
 指定批次中的資料列數目。 此屬性的預設值是 **-1**，表示未指派任何值。  
  
> [!NOTE]  
>  清除 [OLE DB 目的地編輯器]  中的文字方塊，指出您不要指派此屬性的自訂值。  
  
 **插入認可大小上限**  
 指定快速載入作業期間，OLE DB 目的地嘗試認可的批次大小。 預設值 **0** 表示處理所有資料列之後會在單一批次中認可所有資料。  
  
> [!NOTE]  
>  **0** 的值可能會造成封裝停止回應，前提是 OLE DB 目的地和另一個資料流程元件正在更新相同的來源資料表。 若要避免封裝停止回應，請將 **[插入認可大小上限]** 選項設定為 **2147483647**。  
  
 如果您提供此屬性的值，目的地會認可批次中的資料列，這些批次小於 (a) [插入認可大小上限]  或 (b) 目前正在處理之緩衝區中的其餘資料列。  
  
> [!NOTE]  
>  目的地的任何條件約束失敗都會使 [插入認可大小上限]  所定義的整批資料列失敗。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 請選取包含資料表或檢視名稱的變數。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>資料存取模式 = 資料表名稱或檢視名稱變數 - 快速載入)  
 **變數名稱**  
 請選取包含資料表或檢視名稱的變數。  
  
 **新增**  
 使用 [建立資料表]  對話方塊建立新的資料表。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **保留識別**  
 指定載入資料時是否複製識別值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 **false**。  
  
 **保留 Null**  
 指定載入資料時是否複製 Null 值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 **false**。  
  
 **資料表鎖定**  
 指定載入期間是否鎖定資料表。 此屬性的預設值為 **false**。  
  
 **檢查條件約束**  
 指定工作是否檢查條件約束。 此屬性的預設值為 **false**。  
  
 **每批次的資料列**  
 指定批次中的資料列數目。 此屬性的預設值是 **-1**，表示未指派任何值。  
  
> [!NOTE]  
>  清除 [OLE DB 目的地編輯器]  中的文字方塊，指出您不要指派此屬性的自訂值。  
  
 **插入認可大小上限**  
 指定快速載入作業期間，OLE DB 目的地嘗試認可的批次大小。 預設值 **2147483647** 表示處理所有資料列之後會在單一批次中認可所有資料。  
  
> [!NOTE]  
>  **0** 的值可能會造成封裝停止回應，前提是 OLE DB 目的地和另一個資料流程元件正在更新相同的來源資料表。 若要避免封裝停止回應，請將 **[插入認可大小上限]** 選項設定為 **2147483647**。  
  
#### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢文字，按一下 [建立查詢]  建立查詢，或按一下 [瀏覽]  找到包含查詢文字的檔案。  
  
> [!NOTE]  
>  OLE DB 目的地不支援參數。 如果需要執行參數化 INSERT 陳述式，請考慮 OLE DB 命令轉換。 如需相關資訊，請參閱 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)。  
  
 **建立查詢**  
 使用 [查詢產生器]  對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟]  對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
## <a name="ole-db-destination-editor-mappings-page"></a>OLE DB 目的地編輯器 (對應頁面)
  使用 [OLE DB 目的地編輯器]  對話方塊的 [對應]  頁面，將輸入資料行對應至目的地資料行。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 使用拖放作業，即可將資料表中的可用輸入資料行對應到目的地資料行。  
  
 **可用的目的地資料行**  
 檢視可用的目的地資料行清單。 使用拖放作業，即可將資料表中的可用目的地資料行對應到輸入資料行。  
  
 **輸入資料行**  
 檢視所選取的輸入資料行。 您可以選取 [\<忽略>]  移除對應，排除輸出的資料行。  
  
 **目的地資料行**  
 檢視每個可用的目的地資料行，不論是否已經對應。  
  
## <a name="ole-db-destination-editor-error-output-page"></a>OLE DB 目的地編輯器 (錯誤輸出頁面)
  使用 **[OLE DB 目的地編輯器]** 對話方塊的 **[錯誤輸出]** 頁面，來指定錯誤處理選項。  
  
### <a name="options"></a>選項。  
 **輸入/輸出**  
 檢視輸入的名稱。  
  
 **資料行**  
 未使用。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題：** [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 未使用。  
  
 **說明**  
 檢視作業的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="related-content"></a>相關內容  
 [OLE DB 來源](../../integration-services/data-flow/ole-db-source.md)  
  
 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)  
  
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
