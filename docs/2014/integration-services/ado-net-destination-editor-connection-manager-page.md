---
title: ADO NET 目的地編輯器 （連線管理員頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.connection.f1
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 611436db1ea4a69a5c33c7bc2c3c9e92f2a350a3
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382296"
---
# <a name="ado-net-destination-editor-connection-manager-page"></a>ADO NET 目的地編輯器 (連線管理員頁面)
  使用 [ADO NET 目的地編輯器] 對話方塊的 [連線管理員] 頁面，即可選取目的地的 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
 若要深入了解 ADO NET 目的地，請參閱＜ [ADO NET Destination](data-flow/ado-net-destination.md)＞。  
  
 **開啟連線管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 目的地的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 ADO NET 目的地。  
  
3.  在 [ADO NET 目的地編輯器] 中，按一下 [連線管理員]。  
  
## <a name="static-options"></a>靜態選項  
 **[ODBC 目的地編輯器]**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [設定 ADO.NET 連線管理員] 對話方塊建立新的連線管理員。  
  
 **使用資料表或檢視**  
 從清單中選取現有的資料表或檢視，或按一下 [新增] 來建立新的資料表。  
  
 **新增**  
 使用 [建立資料表] 對話方塊來建立新的資料表或檢視。  
  
> [!NOTE]  
>  當您按一下 **[新增]** 時， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **預覽**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
 **在可用時使用大量插入**  
 指定是否要使用 <xref:System.Data.SqlClient.SqlBulkCopy> 介面來改善大量插入作業的效能。  
  
 只有傳回 <xref:System.Data.SqlClient.SqlConnection> 物件的 ADO.NET 提供者才支援使用 <xref:System.Data.SqlClient.SqlBulkCopy> 介面。 .NET Data Provider for SQL Server (SqlClient) 會傳回 <xref:System.Data.SqlClient.SqlConnection> 物件，而自訂提供者則可能傳回 <xref:System.Data.SqlClient.SqlConnection> 物件。  
  
 您可以使用 .NET Data Provider for SQL Server (SqlClient) 連接到 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]。  
  
 如果您選取 [盡可能使用大量插入]，並將 [錯誤] 選項設定為 [重新導向資料列]，目的地重新導向至錯誤輸出的資料批次可能會包含良好的資料列。如需處理大量作業中錯誤的詳細資訊，請參閱[處理資料中的錯誤](data-flow/error-handling-in-data.md)。 如需 [錯誤] 選項的詳細資訊，請參閱 [ADO NET 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/ado-net-destination-editor-error-output-page.md)。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 Sybase 來源資料表包含識別欄位，您就必須使用「執行 SQL」工作，在 ADO NET 目的地前後執行 SET IDENTITY_INSERT 陳述式。 識別欄位屬性會指定資料行的累加值。 SET IDENTITY_INSERT 陳述式可讓明確值插入識別欄位中。 若要在相同的資料庫連接上執行 CREATE TABLE 和 SET IDENTITY 陳述式，請將 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連接管理員的 `RetainSameConnection` 屬性設定為 `True`。 此外，您可以針對「執行 SQL」工作和 ADO NET 目的地使用相同的 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員。  
>   
>  如需詳細資訊，請參閱 [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-identity-insert-transact-sql) 和 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)。  
  
## <a name="external-resources"></a>外部資源  
 sqlcat.com 上的技術文件： [快速將資料載入 Windows Azure SQL 資料庫的方式](https://go.microsoft.com/fwlink/?LinkId=244333)  
  
## <a name="see-also"></a>另請參閱  
 [ADO NET 目的地編輯器 &#40;對應頁面&#41;](../../2014/integration-services/ado-net-destination-editor-mappings-page.md)   
 [ADO NET 目的地編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/ado-net-destination-editor-error-output-page.md)   
 [ADO.NET 連線管理員](connection-manager/ado-net-connection-manager.md)   
 [執行 SQL 工作](control-flow/execute-sql-task.md)  
  
  
