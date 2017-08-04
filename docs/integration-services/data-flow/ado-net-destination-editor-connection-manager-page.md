---
title: "ADO NET 目的地編輯器 （連接管理員頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.adonetdest.connection.f1
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 16ed4103735f389959531b92fad81884fc583a5b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="ado-net-destination-editor-connection-manager-page"></a>ADO NET 目的地編輯器 (連線管理員頁面)
  使用 [ADO NET 目的地編輯器] 對話方塊的 [連線管理員] 頁面，即可選取目的地的 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
 若要深入了解 ADO NET 目的地，請參閱＜ [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md)＞。  
  
 **開啟連線管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟具有 ADO NET 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 ADO NET 目的地。  
  
3.  在 [ADO NET 目的地編輯器] 中，按一下 [連線管理員]。  
  
## <a name="static-options"></a>靜態選項  
 **連線管理員**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [設定 ADO.NET 連線管理員] 對話方塊建立新的連線管理員。  
  
 **使用資料表或檢視**  
 從清單中選取現有的資料表或檢視，或按一下 [新增] 來建立新的資料表。  
  
 **新增**  
 使用 [建立資料表] 對話方塊來建立新的資料表或檢視。  
  
> [!NOTE]  
>  當您按一下 **[新增]**時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **預覽**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
 **在可用時使用大量插入**  
 指定是否要使用 <xref:System.Data.SqlClient.SqlBulkCopy> 介面來改善大量插入作業的效能。  
  
 只有傳回 <xref:System.Data.SqlClient.SqlConnection> 物件的 ADO.NET 提供者才支援使用 <xref:System.Data.SqlClient.SqlBulkCopy> 介面。 .NET Data Provider for SQL Server (SqlClient) 會傳回 <xref:System.Data.SqlClient.SqlConnection> 物件，而自訂提供者則可能傳回 <xref:System.Data.SqlClient.SqlConnection> 物件。  
  
 您可以使用 .NET Data Provider for SQL Server (SqlClient) 連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
  
 如果您選取 [盡可能使用大量插入]，並將 [錯誤] 選項設定為 [重新導向資料列]，目的地重新導向至錯誤輸出的資料批次可能會包含良好的資料列。如需處理大量作業中錯誤的詳細資訊，請參閱[處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。 如需有關**錯誤**選項，請參閱[ADO NET 目的地編輯器 &#40;錯誤輸出頁面 &#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  如果 SQL Server 或 Sybase 來源資料表包含識別欄位，您必須使用執行 SQL 」 工作，才能啟用 IDENTITY_INSERT ADO NET 目的地之前以及將它一次之後停用。 （identity 資料行屬性會指定資料行的累加值。 SET IDENTITY_INSERT 陳述式可讓來源資料表中明確值插入至目的地資料表中的識別欄位。）  
>   
>   若要執行 SET IDENTITY_INSERT 陳述式和資料載入成功，您必須執行下列動作。
>       1. 針對執行 SQL 工作和 ADO.NET 目的地，請使用相同的 ADO.NET 連接管理員。
>       2. 在 連接管理員上設定**RetainSameConnection**屬性和**MultipleActiveResultSets**屬性設定為 True。
>       3. 在 ADO.NET 目的地中，設定**UseBulkInsertWhenPossible**屬性設定為 False。
>
>  如需詳細資訊，請參閱 [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/set-identity-insert-transact-sql.md) 和 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)。  
  
## <a name="external-resources"></a>外部資源  
 sqlcat.com 上的技術文件： [快速將資料載入 Windows Azure SQL 資料庫的方式](http://go.microsoft.com/fwlink/?LinkId=244333)  
  
## <a name="see-also"></a>請參閱＜  
 [ADO NET 目的地編輯器 &#40;對應頁面&#41;](../../integration-services/data-flow/ado-net-destination-editor-mappings-page.md)   
 [ADO NET 目的地編輯器 &#40;錯誤輸出頁面 &#41;](../../integration-services/data-flow/ado-net-destination-editor-error-output-page.md)   
 [ADO.NET 連接管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)   
 [執行 SQL 工作](../../integration-services/control-flow/execute-sql-task.md)  
  
  
