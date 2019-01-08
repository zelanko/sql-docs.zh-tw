---
title: OLE DB 目的地編輯器 （連線管理員頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdestadapter.connection.f1
helpviewer_keywords:
- OLE DB Destination Editor
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7688f3979f935b6d461c47fe2747eb7718835f01
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52504705"
---
# <a name="ole-db-destination-editor-connection-manager-page"></a>OLE DB 目的地編輯器 (連接管理員頁面)
  使用 **[OLE DB 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面來選取目的地的 OLE DB 連接。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
> [!NOTE]  
>  `CommandTimeout` OLE DB 目的地的屬性不適用於**OLE DB 目的地編輯器**，但可以透過設定**進階編輯器**。 此外， **[進階編輯器]** 中只會有特定的快速載入選項。 如需有關這些屬性的詳細資訊，請參閱＜ [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md)＞的＜OLE DB 目的地＞一節。  
  
 若要深入了解 OLE DB 目的地，請參閱＜ [OLE DB Destination](data-flow/ole-db-destination.md)＞。  
  
## <a name="static-options"></a>靜態選項  
 **[無快取]**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [設定 OLE DB 連線管理員] 對話方塊建立新的連線管理員。  
  
 **資料存取模式**  
 指定將資料載入目的地的方法。 請注意，雙位元組字集 (DBCS) 資料需要使用其中一種快速載入選項。 如需有關快速載入資料存取模式 (已針對大量插入進行過最佳化) 的詳細資訊，請參閱＜ [OLE DB Destination](data-flow/ole-db-destination.md)＞。  
  
|選項|描述|  
|------------|-----------------|  
|資料表或檢視|將資料載入 OLE DB 目的地中的資料表或檢視。|  
|資料表或檢視 - 快速載入|將資料載入 OLE DB 目的地中的資料表或檢視，並使用快速載入選項。 如需有關快速載入資料存取模式 (已針對大量插入進行過最佳化) 的詳細資訊，請參閱＜ [OLE DB Destination](data-flow/ole-db-destination.md)＞。|  
|資料表名稱或檢視名稱變數|請在變數中指定資料表或檢視名稱。<br /><br /> **相關的資訊**:[在套件中使用變數](../../2014/integration-services/use-variables-in-packages.md)|  
|資料表名稱或檢視名稱變數 - 快速載入|在變數中指定資料表或檢視名稱，並使用快速載入選項來載入資料。 如需有關快速載入資料存取模式 (已針對大量插入進行過最佳化) 的詳細資訊，請參閱＜ [OLE DB Destination](data-flow/ole-db-destination.md)＞。|  
|SQL (命令)|使用 SQL 查詢，將資料載入到 OLE DB 目的地。|  
  
 **預覽**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
## <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
 **[資料存取模式]** 的每個設定都會顯示該設定專用的動態選項集。 下列章節將一一描述每個 **[資料存取模式]** 設定可用的動態選項。  
  
### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **資料表或檢視的名稱**  
 從資料來源中可用的清單中選取資料表或檢視名稱。  
  
 **新增**  
 使用 [建立資料表] 對話方塊建立新的資料表。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
### <a name="data-access-mode--table-or-view---fast-load"></a>資料存取模式 = 資料表或檢視 - 快速載入  
 **資料表或檢視的名稱**  
 使用此清單從資料庫選取資料表或檢視，或按一下 [新增] 建立新的資料表。  
  
 **新增**  
 使用 [建立資料表] 對話方塊建立新的資料表。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **保留識別**  
 指定載入資料時是否複製識別值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 `false`。  
  
 **保留 Null**  
 指定載入資料時是否複製 Null 值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 `false`。  
  
 **資料表鎖定**  
 指定載入期間是否鎖定資料表。 此屬性的預設值為 `true`。  
  
 **檢查條件約束**  
 指定目的地在載入資料時是否檢查條件約束。 此屬性的預設值為 `true`。  
  
 **每批次的資料列**  
 指定批次中的資料列數目。 此屬性的預設值是 **-1**，表示未指派任何值。  
  
> [!NOTE]  
>  清除 [OLE DB 目的地編輯器] 中的文字方塊，指出您不要指派此屬性的自訂值。  
  
 **插入認可大小上限**  
 指定快速載入作業期間，OLE DB 目的地嘗試認可的批次大小。 預設值 **0** 表示處理所有資料列之後會在單一批次中認可所有資料。  
  
> [!NOTE]  
>  **0** 的值可能會造成封裝停止回應，前提是 OLE DB 目的地和另一個資料流程元件正在更新相同的來源資料表。 若要避免封裝停止回應，請將 **[插入認可大小上限]** 選項設定為 **2147483647**。  
  
 如果您提供此屬性的值，目的地會認可批次中的資料列，這些批次小於 (a) [插入認可大小上限] 或 (b) 目前正在處理之緩衝區中的其餘資料列。  
  
> [!NOTE]  
>  目的地的任何條件約束失敗都會使 [插入認可大小上限] 所定義的整批資料列失敗。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 請選取包含資料表或檢視名稱的變數。  
  
### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>資料存取模式 = 資料表名稱或檢視名稱變數 - 快速載入)  
 **變數名稱**  
 請選取包含資料表或檢視名稱的變數。  
  
 **新增**  
 使用 [建立資料表] 對話方塊建立新的資料表。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **保留識別**  
 指定載入資料時是否複製識別值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 `false`。  
  
 **保留 Null**  
 指定載入資料時是否複製 Null 值。 這個屬性只能搭配快速載入選項使用。 此屬性的預設值為 `false`。  
  
 **資料表鎖定**  
 指定載入期間是否鎖定資料表。 此屬性的預設值為 `false`。  
  
 **檢查條件約束**  
 指定工作是否檢查條件約束。 此屬性的預設值為 `false`。  
  
 **每批次的資料列**  
 指定批次中的資料列數目。 此屬性的預設值是 **-1**，表示未指派任何值。  
  
> [!NOTE]  
>  清除 [OLE DB 目的地編輯器] 中的文字方塊，指出您不要指派此屬性的自訂值。  
  
 **插入認可大小上限**  
 指定快速載入作業期間，OLE DB 目的地嘗試認可的批次大小。 預設值 **2147483647** 表示處理所有資料列之後會在單一批次中認可所有資料。  
  
> [!NOTE]  
>  **0** 的值可能會造成封裝停止回應，前提是 OLE DB 目的地和另一個資料流程元件正在更新相同的來源資料表。 若要避免封裝停止回應，請將 **[插入認可大小上限]** 選項設定為 **2147483647**。  
  
### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢文字，按一下 [建立查詢] 建立查詢，或按一下 [瀏覽] 找到包含查詢文字的檔案。  
  
> [!NOTE]  
>  OLE DB 目的地不支援參數。 如果需要執行參數化 INSERT 陳述式，請考慮 OLE DB 命令轉換。 如需相關資訊，請參閱 [OLE DB Command Transformation](data-flow/transformations/ole-db-command-transformation.md)。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [OLE DB 目的地編輯器 &#40;對應頁面&#41;](../../2014/integration-services/ole-db-destination-editor-mappings-page.md)   
 [OLE DB 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/ole-db-destination-editor-error-output-page.md)   
 [使用 OLE DB 目的地來載入資料](data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  
