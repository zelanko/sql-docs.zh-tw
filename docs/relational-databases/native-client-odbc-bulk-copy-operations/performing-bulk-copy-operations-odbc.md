---
title: 執行大量複製作業（ODBC） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC]
- ODBC, bulk copy operations
- minimally logged operations [SQL Server Native Client]
- bulk copy [ODBC], about bulk copy
ms.assetid: 5c793405-487c-4f52-88b8-0091d529afb3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e58c355c437d325e2a0db228f8ed4af83956fecf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73785040"
---
# <a name="performing-bulk-copy-operations-odbc"></a>執行大量複製作業 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 標準不直接支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大量複製作業。 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 或更新版本的值行個體時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大量複製作業的 DB-Library 函數。 此驅動程式專屬的延伸模組提供一個簡單的升級路徑給使用大量複製函數的現有 DB-Library 應用程式。 特定的大量複製支援位於下列檔案中：  
  
-   sqlncli.h  
  
     包括適用於大量複製函數的函數原型與常數定義。 sqlncli.h 必須包含在執行大量複製作業的 ODBC 應用程式中，而且必須在應用程式編譯時的 include 路徑中。  
  
-   sqlncli11.lib  
  
     必須位於連結器 (Linker) 的程式庫路徑中，並指定為要連結的檔案。 sqlncli11.lib 是透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式散發。  
  
-   sqlncli11.dll  
  
     在執行時間必須存在。 sqlncli11.dll 是透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式散發。  
  
> [!NOTE]  
>  ODBC **SQLBulkOperations**函數與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]大量複製函數沒有任何關聯性。 應用程式必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專用的大量複製函數才能執行大量複製作業。  
  
## <a name="minimally-logging-bulk-copies"></a>最低限度記錄的大量複製  
 利用完整復原模式，大量載入所執行的所有資料列插入作業都會完整記錄在交易記錄檔中。 對於大型資料載入，這可能會導致交易記錄檔迅速填滿。 在某些情況下，可以用最低限度記錄。 最低限度記錄會降低大量載入作業填滿記錄檔空間的可能性，而且也比完整記錄更有效率。  
  
 如需使用最低限度記錄的詳細資訊，請參閱[大量匯入的最低限度記錄的必要條件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。  
  
## <a name="remarks"></a>備註  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本中使用 bcp.exe 時，如果在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前沒有錯誤，則可能會看到錯誤。 這是因為在更新版本中，bcp.exe 不再執行隱含資料類型轉換。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前，如果目標資料表有 money 資料類型，則 bcp.exe 會將數值資料轉換為 money 資料類型。 不過，在這種情況下，bcp.exe 只會截斷額外的欄位。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，當檔案和目標資料表之間的資料類型不符時，如果有任何資料必須截斷才能容納到目標資料表，bcp.exe 將會引發錯誤。 若要解決此錯誤，請修正資料以符合目標資料類型。 或者，使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前版本的 bcp.exe。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用資料檔案與格式檔案](../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
-   [從程式變數中大量複製](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-from-program-variables.md)  
  
-   [管理大量複製批次大小](../../relational-databases/native-client-odbc-bulk-copy-operations/managing-bulk-copy-batch-sizes.md)  
  
-   [大量複製 Text 與 Image 資料](../../relational-databases/native-client-odbc-bulk-copy-operations/bulk-copying-text-and-image-data.md)  
  
-   [從 DB-Library 轉換成 ODBC 大量複製](../../relational-databases/native-client-odbc-bulk-copy-operations/converting-from-db-library-to-odbc-bulk-copy.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
