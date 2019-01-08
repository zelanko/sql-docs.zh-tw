---
title: 使用 BULK INSERT 或 OPENROWSET (BULK...) 匯入大量資料 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1dec3a2821e2b92d431680b49e37a7b9819887b2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505546"
---
# <a name="import-bulk-data-by-using-bulk-insert-or-openrowsetbulk-sql-server"></a>使用 BULK INSERT 或 OPENROWSET(BULK...) 匯入大量資料 (SQL Server)
  本主題提供一個概觀，說明如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT 陳述式與 INSERT...SELECT * FROM OPENROWSET(BULK...) 陳述式，從資料檔案大量匯入資料到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。 本主題也將說明有關使用 BULK INSERT 和 OPENROWSET(BULK…)，以及使用這些方法從遠端資料來源大量匯入時的安全性考量。  
  
> [!NOTE]  
>  當您使用 BULK INSERT 或 OPENROWSET(BULK…) 時，了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本處理模擬的方式相當重要。 如需詳細資訊，請參閱本主題稍後的「安全性考量」。  
  
## <a name="bulk-insert-statement"></a>BULK INSERT 陳述式  
 BULK INSERT 會從資料檔案將資料載入資料表。 此功能與 **bcp** 命令的 **in** 選項相似，但卻是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序來讀取資料檔案。 如需 BULK INSERT 語法的描述，請參閱 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
### <a name="examples"></a>範例  
 如需 BULK INSERT 範例，請參閱：  
  
-   [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)  
  
-   [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [大量匯入資料時保留識別值 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="openrowsetbulk-function"></a>OPENROWSET(BULK…)函數  
 OPENROWSET BULK 資料列集提供者可透過呼叫 OPENROWSET 函數及指定 BULK 選項加以存取。 OPENROWSET(BULK…) 函數可讓您透過 OLE DB 提供者連接到遠端資料來源 (例如資料檔案)，以存取遠端資料。  
  
 若要大量匯入資料，請從 INSERT 陳述式內的 SELECT…FROM 子句呼叫 OPENROWSET(BULK…)。 大量匯入資料的基本語法是：  
  
 INSERT ...SELECT * FROM OPENROWSET(BULK...)  
  
 當用於 INSERT 陳述式時，OPENROWSET(BULK...) 支援資料表提示。 除了一般的資料表提示，例如 TABLOCK，BULK 子句可接受下列特殊化的資料表提示：（忽略 CHECK 條件約束） 的 IGNORE_CONSTRAINTS、 IGNORE_TRIGGERS、 KEEPDEFAULTS 和 KEEPIDENTITY。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)。  
  
 如需 BULK 選項其他用法的資訊，請參閱 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
### <a name="examples"></a>範例  
 如需 INSERT...SELECT * FROM OPENROWSET(BULK...) 陳述式的範例，請參閱下列主題：  
  
-   [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [大量匯入資料時保留識別值 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="security-considerations"></a>安全性考量  
 如果使用者是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，則會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序帳戶的安全性設定檔。 使用 SQL Server 驗證的登入無法於 Database Engine 外部進行驗證。 因此，一旦使用 SQL Server 驗證的登入起始 BULK INSERT 命令，將會使用 SQL Server 處理序帳戶 (即 SQL Server Database Engine 服務所使用的帳戶) 的安全性內容建立與資料的連接。 為了能夠成功讀取來源資料，您必須授與 SQL Server Database Engine 所使用的帳戶對來源資料的存取權。 相反地，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者是使用 Windows 驗證登入，則該使用者只能讀取其使用者帳戶可存取的檔案，而與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的安全性設定檔無關。  
  
 例如，有個使用者使用 Windows 驗證登入了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如果這個使用者要用 BULK INSERT 或 OPENROWSET 從資料檔案匯入資料到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，則使用者帳戶必須具有資料檔案的讀取權限。 有了資料檔案的存取權之後，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序沒有權限存取檔案，使用者還是可以將檔案中的資料匯入到資料表。 使用者不需要將檔案存取權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 可以設定為，透過轉送已驗證 Windows 使用者的認證，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體連接到另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 此設置也稱為「模擬」或「委派」。 當您使用 BULK INSERT 或 OPENROWSET 時，請務必了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本如何處理使用者模擬的安全性。 使用者模擬允許資料檔案位於和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序或使用者不同的電腦上。 例如，如果位於 **Computer_A** 的使用者可以存取 **Computer_B** 上的資料檔案，且已適當設定認證委派，則使用者可以連接到執行於 **Computer_C** 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，然後存取 **Computer_B** 上的資料檔案，並從該檔案大量匯入資料到 **Computer_C** 上的資料表。  
  
## <a name="bulk-importing-from-a-remote-data-file"></a>從遠端資料檔案大量匯入  
 若要使用 BULK INSERT 或 INSERT...SELECT \* FROM OPENROWSET(BULK...) 從另一部電腦大量匯入資料，則必須在兩部電腦之間共用資料檔案。 若要指定共用資料檔案，請使用它的通用命名慣例 (UNC) 名稱，其使用一般格式：**\\\\***Servername***\\***Sharename***\\***Path***\\***Filename*。 此外，用來存取資料檔案的帳戶必須擁有在遠端磁碟上讀取檔案所需的權限。  
  
 例如，下列 `BULK INSERT` 陳述式會從名為 `SalesOrderDetail` 的資料檔案大量匯入資料到 `AdventureWorks` 資料庫的 `newdata.txt`資料表。 此資料檔案位於 `\dailyorders` 系統上的 `salesforce` 網路共用目錄上的 `computer2` 共用資料夾中。  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';  
GO  
```  
  
> [!NOTE]  
>  這個限制並不適用於 **bcp** 公用程式，因為用戶端可以獨立讀取檔案，不受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 影響。  
  
## <a name="see-also"></a>另請參閱  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [SELECT 子句 &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-clause-transact-sql)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FROM &#40;Transact-SQL&#41;](/sql/t-sql/queries/from-transact-sql)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)  
  
  
