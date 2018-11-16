---
title: ADO NET 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetdest.f1
- sql13.dts.designer.adonetdest.connection.f1
- sql13.dts.designer.adonetdest.mappings.f1
- sql13.dts.designer.adonetdest.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 38175416fdd47ee50f9bb3aa94b7318b8926317b
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51640009"
---
# <a name="ado-net-destination"></a>ADO NET 目的地
  ADO NET 目的地會將資料載入使用資料庫資料表或檢視的各種 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]相容資料庫中。 您可以選擇將這些資料載入現有的資料表或檢視中，也可以建立新的資料表並將資料載入新的資料表內。  
  
 您可使用 ADO NET 目的地，連接至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 不過，不支援使用 OLE DB 連接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 如需 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的詳細資訊，請參閱 [Azure SQL Database 一般限制與方針](https://go.microsoft.com/fwlink/?LinkId=248228)。  
  
## <a name="troubleshooting-the-ado-net-destination"></a>ADO NET 目的地疑難排解  
 您可以記錄 ADO NET 目的地對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，針對 ADO NET 目的地所執行之將資料儲存至外部資料來源的作業進行疑難排解。 若要記錄 ADO NET 目的地對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱[封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ado-net-destination"></a>設定 ADO NET 目的地  
 此目的地使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連接管理員以連接到資料來源，且連接管理員會指定要使用的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者。 如需詳細資訊，請參閱 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
 ADO NET 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不需要將輸入資料行對應至所有的目的地資料行。 但是，某些目的地資料行的屬性可能需要對應輸入資料行。 否則，可能會發生錯誤。 例如，如果目的地資料行不允許 Null 值，您必須將輸入資料行對應到該目的地資料行。 此外，對應之資料行的資料類型必須相容。 例如，如果 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 提供者不支援，您就無法將具有字串資料類型的輸入資料行對應至具有數值資料類型的目的地資料行。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援將文字插入資料類型設定為影像的資料行內。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的詳細資訊，請參閱 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)＞。  
  
> [!NOTE]  
>  ADO NET 目的地不支援將類型設定為 DT_DBTIME 的輸入資料行對應至類型設定為日期時間的資料庫資料行。 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 ADO NET 目的地具有一個規則輸入和一個錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO NET 自訂屬性](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="ado-net-destination-editor-connection-manager-page"></a>ADO NET 目的地編輯器 (連線管理員頁面)
  使用 [ADO NET 目的地編輯器] 對話方塊的 [連線管理員] 頁面，即可選取目的地的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
 **開啟連接管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 ADO NET 目的地。  
  
3.  在 [ADO NET 目的地編輯器] 中，按一下 [連線管理員]。  
  
### <a name="static-options"></a>靜態選項  
 **[ODBC 目的地編輯器]**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [設定 ADO.NET 連線管理員] 對話方塊建立新的連線管理員。  
  
 **使用資料表或檢視**  
 從清單中選取現有的資料表或檢視，或按一下 [新增] 來建立新的資料表。  
  
 **新增**  
 使用 [建立資料表] 對話方塊來建立新的資料表或檢視。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **預覽**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
 **在可用時使用大量插入**  
 指定是否要使用 <xref:System.Data.SqlClient.SqlBulkCopy> 介面來改善大量插入作業的效能。  
  
 只有傳回 <xref:System.Data.SqlClient.SqlConnection> 物件的 ADO.NET 提供者才支援使用 <xref:System.Data.SqlClient.SqlBulkCopy> 介面。 .NET Data Provider for SQL Server (SqlClient) 會傳回 <xref:System.Data.SqlClient.SqlConnection> 物件，而自訂提供者則可能傳回 <xref:System.Data.SqlClient.SqlConnection> 物件。  
  
 您可以使用 .NET Data Provider for SQL Server (SqlClient) 連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
  
 如果您選取 [盡可能使用大量插入]，並將 [錯誤] 選項設定為 [重新導向資料列]，目的地重新導向至錯誤輸出的資料批次可能會包含良好的資料列。如需處理大量作業中錯誤的詳細資訊，請參閱[處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。 如需 [錯誤] 選項的詳細資訊，請參閱 [ADO NET 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)。  
  
> [!NOTE]  
>  如果 SQL Server 或 Sybase 來源資料表包含識別欄位，您就必須使用執行 SQL 工作，在 ADO NET 目的地前後啟用及停用 IDENTITY_INSERT 陳述式。 (識別欄位屬性會指定資料行的累加值。 SET IDENTITY_INSERT 陳述式可將來源資料表中的明確值插入至目的地資料表中的識別欄位。)  
>   
>   若要成功執行 SET IDENTITY_INSERT 陳述式並載入資料，您必須執行下列動作。  
>       1.執行 SQL 工作和 ADO NET 目的地要使用相同的 ADO NET 連線管理員。  
>       2.在連線管理員上，將 **RetainSameConnection** 屬性和 **MultipleActiveResultSets** 屬性設定為 True。  
>       3.在 ADO.NET 目的地上，將 **UseBulkInsertWhenPossible** 屬性設為 False。   
>
>  如需詳細資訊，請參閱 [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) 和 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)。  
  
## <a name="external-resources"></a>外部資源  
 sqlcat.com 上的技術文件： [快速將資料載入 Windows Azure SQL 資料庫的方式](https://go.microsoft.com/fwlink/?LinkId=244333)  
  
## <a name="ado-net-destination-editor-mappings-page"></a>ADO NET 目的地編輯器 (對應頁面)
  使用 [ADO NET 目的地編輯器] 對話方塊的 [對應] 頁面，即可將輸入資料行對應至目的地資料行。  
  
 **開啟對應頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 ADO NET 目的地。  
  
3.  在 [ADO NET 目的地編輯器] 中，按一下 [對應]。  
  
### <a name="options"></a>選項。  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 使用拖放作業，即可將資料表中的可用輸入資料行對應到目的地資料行。  
  
 **可用的目的地資料行**  
 檢視可用的目的地資料行清單。 使用拖放作業，即可將資料表中的可用目的地資料行對應到輸入資料行。  
  
 **輸入資料行**  
 檢視所選取的輸入資料行。 您可以選取 [\<忽略>] 移除對應，排除輸出的資料行。  
  
 **目的地資料行**  
 檢視每個可用的目的地資料行，不論是否已經對應。  
  
## <a name="ado-net-destination-editor-error-output-page"></a>ADO NET 目的地編輯器 (錯誤輸出頁面)
  使用 **[ADO NET 目的地編輯器]** 對話方塊的 **[錯誤輸出]** 頁面，即可指定錯誤處理選項。  
  
 **開啟錯誤輸出頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 ADO NET 目的地。  
  
3.  在 **[ADO NET 目的地編輯器]** 中，按一下 **[錯誤輸出]**。  
  
### <a name="options"></a>選項。  
 **輸入或輸出**  
 檢視輸入的名稱。  
  
 **資料行**  
 未使用。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題** [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 未使用。  
  
 **說明**  
 檢視作業的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
  
