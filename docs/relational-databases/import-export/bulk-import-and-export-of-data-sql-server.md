---
title: 資料的大量匯入及匯出 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 26b45540c69237cc8bce4e105dff6d496f3eff0b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39561038"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>資料的大量匯入及匯出 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表匯出大量資料 (「大量資料」)，以及將大量資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或未分割的檢視。 
  
-   *「大量匯出」* 代表將資料從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表複製到資料檔。

-   *「大量匯入」* 代表從資料檔載入資料至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 例如，您可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 應用程式中將資料匯出至資料檔，然後將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。  
 
##  <a name="MethodsForBuliIE"></a> 大量匯入和匯出資料的方法  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表大量匯出資料，以及將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或未分割的檢視。 有下列基本方法可用。  
 
  
|方法|Description|匯入資料|匯出資料|  
|------------|-----------------|------------------|------------------|  
|[bcp 公用程式](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|可大量匯出和大量匯入資料並產生格式檔案的命令列公用程式 (Bcp.exe)。|是|是|  
|[BULK INSERT 陳述式](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，可將資料直接從資料檔案匯入至資料庫資料表或非資料分割的檢視。|是|否|  
|[INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，其指定 OPENROWSET(BULK…) 函數選取 INSERT 陳述式中的資料，以使用 OPENROWSET BULK 資料列集提供者，將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|是|否| 
|[SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)|精靈會建立簡單套件，以在許多常用的資料格式之間匯入和匯出資料，這些格式包括資料庫、試算表和文字檔。|是|是|  
  
> [!IMPORTANT]
> SQL Server 大量匯入作業不支援逗號分隔值 (CSV) 檔案。 不過，在某些情況下，您可以使用 CSV 檔案作為資料檔案，以便將資料大量匯入 SQL Server。 請注意，CSV 檔案的欄位結束字元不必是逗號。 如需詳細資訊，請參閱 [準備大量匯出或匯入的資料 (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)。

> [!NOTE]
> Azure SQL Database 和 Azure SQL DW 只支援使用 bcp 公用程式匯入和匯出分隔的檔案。
  
##  <a name="FFs"></a> 格式檔案  
 [bcp](../../tools/bcp-utility.md) 公用程式、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [INSERT ...SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) 全都支援使用特殊的「格式檔案」，將每一個欄位的格式資訊儲存在資料檔案中。 格式檔案也可以包含對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的相關資訊。 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體大量匯出與大量匯入資料時，格式檔案可以提供所需的所有格式資訊。  
  
 格式檔案提供彈性方式，在匯入期間用於解譯資料檔中的資料，以及在匯出期間用於格式化資料檔中的資料。 這樣的彈性讓您不需撰寫特殊用途的程式碼來解譯資料，也不需因應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或外部應用程式的特定需求將資料重新格式化。 例如，如果您大量匯出的資料即將要載入到需要逗號分隔值的應用程式中，則可以使用格式檔案，在匯出的資料中插入逗號當做欄位結束字元。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援下列兩種類型的格式檔案：XML 格式檔案和非 XML 格式檔案。  
  
 [bcp 公用程式](../../tools/bcp-utility.md) 是唯一可以產生格式檔案的工具。 如需詳細資訊，請參閱[建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)。 如需格式檔案的詳細資訊，請參閱[匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)。  
  
> [!NOTE]
> 萬一在大量匯出或匯入作業期間未提供格式檔案，您可以在命令列覆寫預設格式。

|相關主題|
|---|
|[準備大量匯出或匯入的資料 (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)|
|[大量匯入或大量匯出的資料格式 (SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)<br />&emsp;&#9679;&emsp;[使用原生格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用字元格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用 Unicode 原生格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用 Unicode 字元格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[從舊版 SQL Server 匯入原生與字元格式資料](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)|
|[使用 bcp 指定相容性的資料格式 (SQL Server)](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[使用 bcp 指定檔案儲存類型 (SQL Server)](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[使用 bcp 指定資料檔的前置長度 (SQL Server)](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[使用 bcp 指定欄位長度 (SQL Server)](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[指定欄位與資料列結束字元 (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)|
|[大量匯入期間保留 Null 或使用預設值 (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)|
|[大量匯入資料時保留識別值 (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)|
|[匯入或匯出資料的格式檔案 (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)<br />&emsp;&#9679;&emsp;[建立格式檔案 (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案大量匯入資料 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案略過資料表資料行 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案略過資料欄位 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案將資料表資料行對應至資料檔案的欄位 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)|
 
  
## <a name="more-information"></a>詳細資訊！  
 [大量匯入採用最低限度記錄的必要條件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [複製資料庫至其他伺服器](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [執行 XML 資料的大量載入 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [執行大量複製作業](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)   

  
  
