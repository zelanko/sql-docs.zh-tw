---
title: 啟用 Multiple Active Result Set
description: 討論如何搭配使用 MARS 與 SQL Server。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d0c40df5ec7648b7073f9efa369428b8d88f6d11
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452222"
---
# <a name="enabling-multiple-active-result-sets"></a>啟用 Multiple Active Result Set

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Multiple Active Result Set (MARS) 是與 SQL Server 搭配使用的功能，允許在單一連線中執行多個批次作業。 在啟用 MARS 以與 SQL Server 搭配使用時，使用的每個命令物件都會在連線中新增工作階段。  
  
> [!NOTE]
>  單一 MARS 會話會開啟一個邏輯連線以供 MARS 使用，然後針對每個作用中的命令建立一個邏輯連線。  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>在連接字串中啟用和停用 MARS  
  
> [!NOTE]
>  下列連接字串使用包含於 SQL Server 的 **AdventureWorks** 範例資料庫。 提供的連接字串假設資料庫安裝在名為 MSSQL1 的伺服器上。 視環境需要修改連接字串。  
  
此 MARS 功能預設為停用。 將 "MultipleActiveResultSets = True" 關鍵字組新增至您的連接字串，即可加以啟用。 "True" 是啟用 MARS 的唯一有效值。 下列範例示範如何連接到 SQL Server 的實例，以及如何指定應該啟用 MARS。 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
您可以藉由將 "MultipleActiveResultSets = False" 關鍵字組新增至您的連接字串來停用 MARS。 "False" 是停用 MARS 的唯一有效值。 下列連接字串示範如何停用 MARS。  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>使用 MARS 時的特殊考慮  
一般來說，現有的應用程式不應該進行修改，就能使用啟用 MARS 的連接。 不過，如果您想要在應用程式中使用 MARS 功能，您應該瞭解下列特殊考慮。  
  
### <a name="statement-interleaving"></a>陳述式交錯  
MARS 作業會在伺服器上以同步方式執行。 允許 SELECT 和 BULK INSERT 語句的語句交錯。 但是，資料操作語言（DML）和資料定義語言（DDL）語句會以不可部分完成的方式執行。 在執行不可部分完成的批次時，任何嘗試執行的語句都會被封鎖。 伺服器上的平行執行不是 MARS 功能。  
  
如果在 MARS 連接下提交兩個批次，其中一個包含 SELECT 語句，另一個包含 DML 語句，則 DML 可以在執行 SELECT 語句內開始執行。 不過，必須先執行 DML 語句才能完成，SELECT 語句才會開始進行。 如果這兩個語句都是在相同交易下執行，則在 SELECT 語句啟動之後，DML 語句所做的任何變更都不會顯示在讀取作業中。  
  
在 SELECT 語句內的 WAITFOR 語句不會在等候時產生交易，也就是在產生第一個資料列之前。 這表示在 WAITFOR 語句等候時，不能在相同的連接內執行其他批次。  
  
### <a name="mars-session-cache"></a>MARS 會話快取  
當已啟用 MARS 的連線開啟時，會建立邏輯會話，這會增加額外的負荷。 為了將負荷最小化並提高效能，**SqlClient** 會快取連線內的 MARS 工作階段。 快取包含最多10個 MARS 會話。 這個值不是使用者可調整的。 如果達到會話限制，則會建立新的會話，而不會產生錯誤。 其中包含的快取和會話為每個連接;它們不會在連接之間共用。 當會話發行時，除非已達到集區的上限，否則會將它傳回給集區。 如果快取集區已滿，會話就會關閉。 MARS 會話不會過期。 只有在處置連線物件時，才會清除它們。 MARS 會話快取未預先載入。 因為應用程式需要更多會話，所以會載入它。  
  
### <a name="thread-safety"></a>執行緒安全性  
MARS 作業不是安全線程。  
  
### <a name="connection-pooling"></a>連線共用  
已啟用 MARS 的連接會與任何其他連線共用。 如果應用程式開啟兩個連接，一個已啟用 MARS，另一個已停用 MARS，則兩個連接會在不同的集區中。
  
### <a name="sql-server-batch-execution-environment"></a>SQL Server 批次執行環境  
當連接開啟時，會定義預設的環境。 然後將此環境複製到邏輯 MARS 會話。  
  
批次執行環境包含下列元件：  
  
- Set 選項（例如，ANSI_NullS、DATE_FORMAT、LANGUAGE、TEXTSIZE）  
  
- 安全性內容（使用者/應用程式角色）  
  
- 資料庫內容（目前的資料庫）  
  
- 執行狀態變數（例如，@ @ERROR、@ @ROWCOUNT、@ @FETCH_STATUS @ @IDENTITY）  
  
- 最上層暫存資料表  
  
若使用 MARS，預設的執行環境會與連接產生關聯。 針對指定連線而開始執行的每一個新批次，都會收到預設環境的複本。 每當在指定的批次中執行程式碼時，對環境所做的所有變更都會限定于特定的批次。 執行完成之後，執行設定就會複製到預設環境中。 在單一批次發出多個命令以順序在相同交易下執行的情況下，語義與先前用戶端或伺服器的連接所公開的相同。  
  
### <a name="parallel-execution"></a>平行執行  
MARS 並非設計來移除應用程式中多個連接的所有需求。 如果應用程式需要對伺服器進行真正的平行執行命令，則應該使用多個連接。  
  
例如，假設有以下案例。 建立兩個命令物件，一個用於處理結果集，另一個用於更新資料;它們會透過 MARS 共用共同的連線。 在此案例中，`Transaction`.`Commit` 會無法更新，直到第一個命令物件上的全部結果均讀取完畢，並產生下列例外狀況：  
  
訊息：交易內容正由另一個工作階段所使用。  
  
來源： Microsoft SqlClient Data Provider  
  
應為：（null）  
  
Received： SqlClient. SqlException  
  
有三個選項可處理這種情況：  
  
- 在建立讀取器之後啟動交易，使其不屬於交易的一部分。 接著，每個更新都會變成自己的交易。  
  
- 在讀取器關閉後認可所有工作。 這可能會有大量的更新批次。  
  
- 不要使用 MARS;相反地，請針對每個命令物件使用個別的連接，就像您在 MARS 之前所做的一樣。  
  
### <a name="detecting-mars-support"></a>偵測 MARS 支援  
應用程式可以藉由讀取 `SqlConnection.ServerVersion` 值來檢查 MARS 支援。 SQL Server 2005 的主要數位應為9，SQL Server 2008 則為10。  
  
## <a name="next-steps"></a>後續步驟
- [Multiple Active Result Set (MARS)](multiple-active-result-sets-mars.md)
