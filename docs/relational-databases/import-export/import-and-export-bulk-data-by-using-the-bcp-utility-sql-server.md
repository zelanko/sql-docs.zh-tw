---
title: 使用 bcp 匯入和匯出大量資料
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 09/28/2016
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 521ef35d9d06244c36395e96ab681a21abffe6ea
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74055989"
---
# <a name="import-and-export-bulk-data-using-bcp-sql-server"></a>使用 bcp 匯入和匯出大量資料 (SQL Server)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本主題提供有關使用 [bcp 公用程式](../../tools/bcp-utility.md) ，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫任何執行 SELECT 陳述式的位置 (包括資料分割檢視) 匯出資料的概觀。  
  
 bcp 公用程式 (Bcp.exe) 是使用大量複製程式 (BCP) API 的命令列工具。 bcp 公用程式可執行以下工作：  
  
-   從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表將資料大量匯出到資料檔案。  
  
-   從查詢大量匯出資料。  
  
-   從資料檔案將資料大量匯入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
-   產生格式檔案。  
  
 bcp 公用程式是透過 **bcp** 命令進行存取。 除非使用預先存在的格式檔案，否則您必須了解資料表結構描述及其資料行的資料類型，才能使用 **bcp** 命令大量匯入資料。  
  
 bcp 公用程式可以將資料從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表匯出至資料檔，以供其他程式使用。 此公用程式也可以從另一個程式將資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，通常是從另一個資料庫管理系統 (DBMS) 匯入。 資料會先從來源程式匯出到資料檔案，接著再以個別的作業，從資料檔案複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
 **bcp** 命令提供參數，用來指定資料檔的資料類型及其他資訊。 如果未指定這些參數，命令會提示您輸入格式資訊，例如資料檔案中的資料欄位類型。 此命令會接著詢問您是否想要建立包含互動式回應的格式檔案。 如果想要讓未來的大量匯入或大量匯出作業具有彈性，格式檔案通常會很有用。 您可以在稍後的 **bcp** 命令上，對相等的資料檔指定格式檔案。 如需詳細資訊，請參閱[使用 bcp 時指定相容性的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)。  
  
>**注意！** bcp 公用程式是透過使用 ODBC 大量複製撰寫的。
  
 如需 **bcp** 命令語法的描述，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)。  
  
## <a name="examples"></a>範例  

|下列主題包含使用 bcp 的範例： |
|---|
|[bcp 公用程式](../../tools/bcp-utility.md)<br /><br />大量匯入或大量匯出的資料格式 (SQL Server)<br />&emsp;&#9679;&emsp;[使用原生格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用字元格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用 Unicode 原生格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用 Unicode 字元格式匯入或匯出資料 (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[指定欄位與資料列結束字元 (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[大量匯入期間保留 Null 或使用預設值 (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[大量匯入資料時保留識別值 (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />匯入或匯出資料的格式檔案 (SQL Server)<br />&emsp;&#9679;&emsp;[建立格式檔案 (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案大量匯入資料 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案略過資料表資料行 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案略過資料欄位 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[使用格式檔案將資料表資料行對應至資料檔案的欄位 (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[大量匯入與匯出 XML 文件的範例 (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

## <a name="more-examples-and-information"></a>更多範例和資訊

- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)

- [SELECT 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)

- [bcp 公用程式](../../tools/bcp-utility.md)

- [準備大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-to-bulk-import-data-sql-server.md)

- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)

- [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)

- [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)

- [建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)