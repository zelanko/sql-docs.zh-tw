---
title: "SQL 目的地編輯器 （連接管理員頁面） |Microsoft 文件"
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
- sql13.dts.designer.sqlserverdestadapter.connection.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 423e1654-54af-47c6-ab6f-98670534557d
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb0665ca794b028e2cdb3fd16f6e9514fe9bd33e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="sql-destination-editor-connection-manager-page"></a>SQL 目的地編輯器 (連接管理員頁面)
  使用 **[SQL 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，即可指定資料來源資訊並預覽結果。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地會將資料載入到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料表或檢視。  
  
 若要深入了解 SQL Server 目的地，請參閱＜ [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md)＞。  
  
## <a name="options"></a>選項。  
 **OLE DB 連接管理員**  
 從清單中選取現有的連接，或按一下 [新增] 來建立新的連接。  
  
 **新增**  
 使用 [設定 OLE DB 連線管理員] 對話方塊來建立新的連線。  
  
 **使用資料表或檢視**  
 從清單中選取現有的資料表或檢視，或按一下 [新增] 來建立新的連接。  
  
 **新增**  
 使用 [建立資料表] 對話方塊建立新的資料表。  
  
> [!NOTE]  
>  當您按一下 **[新增]**時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **預覽**  
 使用 [預覽查詢結果] 對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [SQL 目的地編輯器 &#40;[對應] 頁面 &#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [SQL 目的地編輯器 &#40;進階的頁面 &#41;](../../integration-services/data-flow/sql-destination-editor-advanced-page.md)   
 [使用 SQL Server 目的地來大量載入資料](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
