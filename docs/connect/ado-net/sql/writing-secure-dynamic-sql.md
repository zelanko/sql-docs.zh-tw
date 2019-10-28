---
title: 在 SQL Server 中撰寫安全的動態 SQL
description: 說明使用預存程式撰寫安全動態 SQL 的技術。
ms.date: 09/26/2019
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: dd7b76e3333d51a94d6f215a6608511629f35fbe
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451868"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>在 SQL Server 中撰寫安全的動態 SQL

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL 插入式攻擊是指惡意使用者輸入 Transact-sql 語句，而不是有效輸入的程式。 如果在未驗證的情況下將輸入直接傳遞至伺服器，而且應用程式不慎執行插入的程式碼，則攻擊可能會損害或損毀資料。  
  
建構 SQL 陳述式的任何程序都應該經過檢閱，以確認有無插入弱點，因為 SQL Server 會執行收到的所有語法有效查詢。 即使是參數化資料也可能被技術純熟又執意操作的攻擊者操縱。 如果您使用動態 SQL，請務必將命令參數化，且絕不會將參數值直接包含在查詢字串中。  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>SQL 插入式攻擊的剖析  
資料隱碼處理的運作方式是不當地終止文字字串並附加新命令。 因為插入的命令在執行之前可能附加有其他字串，所以不懷好意的人會使用註解標記 "--" 終止插入的字串。 在執行時，後續文字便會被忽略。 可以使用分號插入多個命令（;)為止.  
  
只要插入的 SQL 程式碼語法正確，就無法以程式設計方式偵測竄改。 因此，您必須驗證所有使用者輸入，並且仔細檢視在您使用的伺服器中執行建構之 SQL 命令的程式碼。 絕不串連未經驗證的使用者輸入。 字串串連是指令碼資料隱碼的主要進入點。  
  
以下是一些實用的指導方針：  
  
- 絕對不要直接從使用者輸入建立 Transact-sql 語句;使用預存程式來驗證使用者輸入。  
  
- 透過測試類型、長度、格式和範圍，驗證使用者輸入。 使用 Transact-sql QUOTENAME （）函式來 escape 系統名稱或 REPLACE （）函式，以將字串中的任何字元轉義。  
  
- 在應用程式的每一層中執行多層驗證。  
  
- 測試輸入的大小和資料類型，並強制執行適當的限制。 這有助於防止蓄意的緩衝區滿溢。  
  
- 測試字串變數的內容，僅接受預期的值。 拒絕包含二進位資料、逸出序列和註解字元的項目。  
  
- 使用 XML 文件時，在輸入資料時即驗證所有資料的結構描述。  
  
- 在多層環境中，所有資料應在進入受信任區域之前進行驗證。  
  
- 在可用以建構檔案名稱的欄位中，不接受下列字串：AUX、CLOCK$、COM1 到 COM8、CON、CONFIG$、LPT1 到 LPT8、NUL 和 PRN。  
  
- 搭配使用 <xref:Microsoft.Data.SqlClient.SqlParameter> 物件與預存程式和命令，以提供類型檢查和長度驗證。  
  
- 在用戶端程式代碼中使用 <xref:System.Text.RegularExpressions.Regex> 運算式來篩選不正確字元。  
  
## <a name="dynamic-sql-strategies"></a>動態 SQL 策略  
在程式碼中執行動態建立的 SQL 語句會中斷擁有權鏈，使 SQL Server 檢查呼叫端的許可權是否符合動態 SQL 所存取的物件。  
  
SQL Server 具有一些方法，可使用執行動態 SQL 的預存程序和使用者定義函式來授與資料存取權給使用者。  
  
- 使用模擬搭配 Transact-SQL EXECUTE AS 子句。  
  
- 使用憑證簽署預存程序。  
  
### <a name="execute-as"></a>EXECUTE AS  
EXECUTE AS 子句會將呼叫端的許可權取代為 EXECUTE AS 子句中指定之使用者的許可權。 在 proxy 使用者的安全性內容下執行的嵌套預存程式或觸發程式。 這可能會中斷依賴資料列層級安全性或需要進行審核的應用程式。 某些會傳回使用者身分識別的函式會傳回 EXECUTE AS 子句中指定的使用者，而不是原始呼叫者。 只有在執行程式或發出 REVERT 語句時，才會將執行內容還原到原始呼叫端。  
  
### <a name="certificate-signing"></a>憑證簽署  
當使用憑證簽署的預存程式執行時，授與憑證使用者的許可權會與呼叫者合併。 執行內容維持不變;憑證使用者不會模擬呼叫者。 簽署預存程式需要執行數個步驟。 每次修改程式時，都必須重新簽署程式。  
  
### <a name="cross-database-access"></a>跨資料庫存取  
在執行動態建立的 SQL 語句的情況下，跨資料庫擁有權連結無法運作。 您可以在 SQL Server 中建立存取其他資料庫資料的預存程序，並使用存在於兩個資料庫中的憑證來簽署程序，藉此解決上述問題。 這可讓使用者存取程式所使用的資料庫資源，而不需授與資料庫存取權或許可權。  
  
## <a name="external-resources"></a>外部資源  
如需詳細資訊，請參閱下列資源。  
  
|資源|Description|  
|--------------|-----------------|  
|《SQL Server 線上叢書》中的[預存程序](../../../relational-databases/stored-procedures/stored-procedures-database-engine.md)和 [SQL 資料隱碼](../../../relational-databases/security/sql-injection.md)|主題描述如何建立預存程式，以及 SQL 插入式的運作方式。|  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的應用程式安全性案例](application-security-scenarios-sql-server.md)
