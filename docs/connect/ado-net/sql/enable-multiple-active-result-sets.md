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
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: adcedcdfd0c8909d6834c25df8f03a9b5dc2fa5d
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896957"
---
# <a name="enabling-multiple-active-result-sets"></a>啟用 Multiple Active Result Set

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Multiple Active Result Set (MARS) 是與 SQL Server 搭配使用的功能，允許在單一連線中執行多個批次作業。 在啟用 MARS 以與 SQL Server 搭配使用時，使用的每個命令物件都會在連線中新增工作階段。  
  
> [!NOTE]
>  單一 MARS 工作階段會開啟一個邏輯連線以供 MARS 使用，然後針對每個使用中的命令建立一個邏輯連線。  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>在連接字串中啟用和停用 MARS  
  
> [!NOTE]
>  下列連接字串使用包含於 SQL Server 的 **AdventureWorks** 範例資料庫。 提供的連接字串假設資料庫已安裝於名為 MSSQL1 的伺服器上。 請依據您的環境需求修改連接字串。  
  
此 MARS 功能預設為停用。 將 "MultipleActiveResultSets=True" 關鍵字組新增至連接字串，即可加以啟用。 "True" 是啟用 MARS 的唯一有效值。 下列範例示範如何連線到 SQL Server 的執行個體，以及如何指定應該啟用 MARS。 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
您可以藉由將 "MultipleActiveResultSets=False" 關鍵字組新增至連接字串來停用 MARS。 "False" 是停用 MARS 的唯一有效值。 下列連接字串示範如何停用 MARS。  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>使用 MARS 時的特殊考量  
一般來說，現有的應用程式應該不需要修改，就能使用已啟用 MARS 的連線。 不過，如果您想要在應用程式中使用 MARS 功能，就應該了解下列特殊考量。  
  
### <a name="statement-interleaving"></a>陳述式交錯  
MARS 作業會在伺服器上同步執行。 允許 SELECT 和 BULK INSERT 陳述式的陳述式交錯。 但是，資料操作語言 (DML) 和資料定義語言 (DDL) 陳述式會以不可部分完成的方式執行。 在執行不可部分完成的批次時，任何嘗試執行的陳述式都會遭到封鎖。 在伺服器上平行執行不是 MARS 功能。  
  
如果在 MARS 連線下提交兩個批次，其中一個包含 SELECT 陳述式，另一個包含 DML 陳述式，則 DML 可以在 SELECT 陳述式執行期間開始執行。 不過，DML 陳述式必須先執行完成，SELECT 陳述式才可取得進展。 如果這兩個陳述式都是在相同交易下執行，則讀取作業看不到 DML 陳述式在 SELECT 陳述式開始執行之後所做的任何變更。  
  
SELECT 陳述式內的 WAITFOR 陳述式不會在等候時 (也就是在產生第一個資料列之前) 產生交易。 這表示在 WAITFOR 陳述式等候時，無法在相同連線內執行任何其他批次。  
  
### <a name="mars-session-cache"></a>MARS 工作階段快取  
開啟已啟用 MARS 的連線時，即會建立邏輯工作階段，而這會增加額外負荷。 為了將負荷最小化並提高效能，**SqlClient** 會快取連線內的 MARS 工作階段。 快取最多包含 10 個 MARS 工作階段。 使用者無法調整此值。 如果達到工作階段限制，即會建立新的工作階段，而不會產生錯誤。 其中所含的快取和工作階段都會以每個連線為基礎；它們不會在連線之間共用。 釋放工作階段時，除非已達集區上限，否則會將它傳回給該集區。 如果快取集區已滿，就會關閉工作階段。 MARS 工作階段不會過期。 只有在處置連線物件時，才會清除它們。 MARS 工作階段快取並未預先載入。 它會因為應用程式需要更多工作階段而載入。  
  
### <a name="thread-safety"></a>執行緒安全性  
MARS 作業不是安全執行緒。  
  
### <a name="connection-pooling"></a>連線共用  
已啟用 MARS 的連線就像任何其他連線一樣都是集區式的。 如果應用程式開啟兩個連線，一個已啟用 MARS，另一個已停用 MARS，則這兩個連線會位於不同的集區。
  
### <a name="sql-server-batch-execution-environment"></a>SQL Server 批次執行環境  
開啟連線時，即會定義預設的環境。 接著會將此環境複製到邏輯 MARS 工作階段。  
  
批次執行環境包括下列元件：  
  
- 設定選項 (例如，ANSI_NULLS、DATE_FORMAT、LANGUAGE、TEXTSIZE)  
  
- 資訊安全內容 (使用者/應用程式角色)  
  
- 資料庫內容 (目前的資料庫)  
  
- 執行狀態變數 (例如，@@ERROR、@@ROWCOUNT、@@FETCH_STATUS @@IDENTITY)  
  
- 最上層暫存資料表  
  
使用 MARS，預設執行環境就會與連線產生關聯。 針對指定連線而開始執行的每一個新批次，都會收到預設環境的複本。 每當在指定批次中執行程式碼時，對環境所做的所有變更範圍都會侷限於該特定批次。 執行完成之後，執行設定就會複製到預設環境中。 如果是在相同交易下發出數個要循序執行之命令的單一批次，則語意會與涉及早期用戶端或伺服器之連線所公開的語意相同。  
  
### <a name="parallel-execution"></a>平行執行  
MARS 並非設計來移除應用程式中有多個連線的所有需求。 如果應用程式需要對伺服器進行真正的命令平行執行，就應該使用多個連線。  
  
例如，請設想下列情況。 已建立兩個命令物件，一個用於處理結果集，另一個則用於更新資料；它們會透過 MARS 共用一般連線。 在此案例中，`Transaction`.`Commit` 會無法更新，直到第一個命令物件上的全部結果均讀取完畢，並產生下列例外狀況：  
  
訊息：交易內容正由另一個工作階段所使用。  
  
來源：Microsoft SqlClient Data Provider  
  
預期：(Null)  
  
已收到：Microsoft.Data.SqlClient.SqlException  
  
有三個選項可用來處理此案例：  
  
- 建立讀取器之後啟動交易，因此它不屬於交易的一部分。 接著，每個更新都會變成它自己的交易。  
  
- 在讀取器關閉後認可所有工作。 這可能會有大量的更新批次。  
  
- 不要使用 MARS，而是針對每個命令物件改為使用個別連線，就像您在 MARS 之前所做的一樣。  
  
### <a name="detecting-mars-support"></a>偵測 MARS 支援  
應用程式可以藉由讀取 `SqlConnection.ServerVersion` 值來檢查 MARS 支援。 SQL Server 2005 的主要版本號碼應為 9，而 SQL Server 2008 的則為 10。  
  
## <a name="next-steps"></a>後續步驟
- [Multiple Active Result Set (MARS)](multiple-active-result-sets-mars.md)
