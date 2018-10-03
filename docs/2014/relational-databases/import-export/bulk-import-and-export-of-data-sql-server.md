---
title: 資料的大量匯入及匯出 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36065984f03980f54cbc6a75162bb007f8b5f772
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124438"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>資料的大量匯入及匯出 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表匯出大量資料 (「大量資料」)，以及將大量資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或未分割的檢視。 大量匯入和大量匯出對於在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與異質資料來源間有效傳送資料，是必要條件。 *「大量匯出」* 代表將資料從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表複製到資料檔。 *「大量匯入」* 代表從資料檔載入資料至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 例如，您可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 應用程式中將資料匯出至資料檔，然後將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。  
  
 **本主題內容：**  
  
-   [大量匯入和大量匯出作業簡介](#Intro)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="Intro"></a> 大量匯入和大量匯出概觀  
 本節列出並簡要比較各種適用於大量匯入和匯出資料的方法。 本節也介紹格式檔案。  
  
 **本主題內容：**  
  
-   [大量匯入和匯出資料的方法](#MethodsForBuliIE)  
  
-   [格式檔案](#FFs)  
  
###  <a name="MethodsForBuliIE"></a> 大量匯入和匯出資料的方法  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表大量匯出資料，以及將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或未分割的檢視。 有下列基本方法可用。  
  
|方法|描述|匯入資料|匯出資料|  
|------------|-----------------|------------------|------------------|  
|[bcp 公用程式](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|可大量匯出和大量匯入資料並產生格式檔案的命令列公用程式 (Bcp.exe)。|是|是|  
|[BULK INSERT 陳述式](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，可將資料直接從資料檔案匯入至資料庫資料表或非資料分割的檢視。|是|否|  
|[INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，其指定 OPENROWSET(BULK…) 函數選取 INSERT 陳述式中的資料，以使用 OPENROWSET BULK 資料列集提供者，將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|是|否|  
  
> [!IMPORTANT]  
>  SQL Server 大量匯入作業不支援逗號分隔值 (CSV) 檔案。 不過，在某些情況下，CSV 檔案可用以當做資料檔，以便將資料大量匯入 SQL Server。 請注意，CSV 檔案的欄位結束字元不必是逗號。 如需詳細資訊，請參閱[準備大量匯出或匯入的資料 &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)。  
  
###  <a name="FFs"></a> 格式檔案  
 **bcp** 公用程式、BULK INSERT 和 INSERT ...SELECT \* FROM OPENROWSET(BULK...) 全都支援使用特殊的「格式檔案」，將每一個欄位的格式資訊儲存在資料檔案中。 格式檔案也可以包含對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的相關資訊。 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體大量匯出與大量匯入資料時，格式檔案可以提供所需的所有格式資訊。  
  
 格式檔案提供彈性方式，在匯入期間用於解譯資料檔中的資料，以及在匯出期間用於格式化資料檔中的資料。 這樣的彈性讓您不需撰寫特殊用途的程式碼來解譯資料，也不需因應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或外部應用程式的特定需求將資料重新格式化。 例如，如果您大量匯出的資料即將要載入到需要逗號分隔值的應用程式中，則可以使用格式檔案，在匯出的資料中插入逗號當做欄位結束字元。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援下列兩種類型的格式檔案：XML 格式檔案和非 XML 格式檔案。  
  
 **bcp** 公用程式是唯一可以產生格式檔案的工具。 如需詳細資訊，請參閱[建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)。 如需格式檔案的詳細資訊，請參閱[匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
> [!NOTE]  
>  萬一在大量匯出或匯入作業期間未提供格式檔案，您可以在命令列覆寫預設格式。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [匯入和匯出大量資料使用 bcp 公用程式&#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)  
  
-   [使用 BULK INSERT 或 OPENROWSET 大量資料匯入&#40;大量...&#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)  
  
-   [大量匯入資料時保留識別值 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [準備大量匯出或匯入的資料 &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **若要使用格式檔案**  
  
-   [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **若要在使用 bcp 時指定相容性的資料格式**  
  
1.  [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [使用 bcp 指定檔案儲存類型 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [大量匯入採用最低限度記錄的必要條件](prerequisites-for-minimal-logging-in-bulk-import.md)   
 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [複製資料庫至其他伺服器](../databases/copy-databases-to-other-servers.md)   
 [執行 XML 資料的大量載入 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [執行大量複製作業](../native-client/features/performing-bulk-copy-operations.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
