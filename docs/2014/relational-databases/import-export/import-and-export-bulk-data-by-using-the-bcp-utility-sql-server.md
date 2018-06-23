---
title: 使用 bcp 公用程式匯入及匯出大量資料 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c16ceceac2f4ddfed82605e18cac30f15894d702
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146743"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>使用 bcp 公用程式匯入及匯出大量資料 (SQL Server)
  本主題提供有關使用 [bcp 公用程式](../../tools/bcp-utility.md)，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫任何執行 SELECT 陳述式的位置 (包括資料分割檢視) 匯出資料的概觀。  
  
 bcp 公用程式 (Bcp.exe) 是使用大量複製程式 (BCP) API 的命令列工具。 bcp 公用程式可執行以下工作：  
  
-   從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表將資料大量匯出到資料檔案。  
  
-   從查詢大量匯出資料。  
  
-   從資料檔案將資料大量匯入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
-   產生格式檔案。  
  
 bcp 公用程式是透過 **bcp** 命令進行存取。 除非使用預先存在的格式檔案，否則您必須了解資料表結構描述及其資料行的資料類型，才能使用 **bcp** 命令大量匯入資料。  
  
 bcp 公用程式可以將資料從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表匯出至資料檔，以供其他程式使用。 此公用程式也可以從另一個程式將資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，通常是從另一個資料庫管理系統 (DBMS) 匯入。 資料會先從來源程式匯出到資料檔案，接著再以個別的作業，從資料檔案複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
 **bcp** 命令提供參數，用來指定資料檔的資料類型及其他資訊。 如果未指定這些參數，命令會提示您輸入格式資訊，例如資料檔案中的資料欄位類型。 此命令會接著詢問您是否想要建立包含互動式回應的格式檔案。 如果想要讓未來的大量匯入或大量匯出作業具有彈性，格式檔案通常會很有用。 您可以在稍後的 **bcp** 命令上，對相等的資料檔指定格式檔案。 如需詳細資訊，請參閱[使用 bcp 指定相容性的資料格式 &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)。  
  
> [!NOTE]  
>  bcp 公用程式是透過使用 ODBC 大量複製撰寫的。  
  
 如需 **bcp[ 命令語法的描述，請參閱** bcp 公用程式](../../tools/bcp-utility.md)。  
  
## <a name="examples"></a>範例  
 如需 **bcp** 範例，請參閱：  
  
-   [bcp 公用程式](../../tools/bcp-utility.md)  
  
-   [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [大量匯入資料時保留識別值 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [SELECT 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [準備大量匯入資料 &#40;SQL Server&#41;](prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
  
