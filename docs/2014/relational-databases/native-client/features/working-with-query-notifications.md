---
title: 使用查詢通知 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], query notifications
- rowsets [SQL Server], notifications
- SQL Server Native Client, query notifications
- notifications [SQL Server Native Client]
- query notifications [SQL Server], SQL Server Native Client
- canceling rowset changes
- IRowsetNotify interface
- SQLNCLI, query notifications
- SQL Server Native Client OLE DB provider, query notifications
- consumer notification for rowset changes [SQL Server Native Client]
ms.assetid: 2f906fff-5ed9-4527-9fd3-9c0d27c3dff7
author: rothja
ms.author: jroth
ms.openlocfilehash: ba30bfc8df05a55e297ae8fcb8e2253de57e3ca6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038953"
---
# <a name="working-with-query-notifications"></a>使用查詢通知
  查詢通知是在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中引進。 查詢通知是根據 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引進的 Service Broker 基礎結構而建置，可讓應用程式在資料變更時收到通知。 此功能對於從資料庫中提供資訊快取的應用程式 (如 Web 應用程式)，及需要在來源資料變更時收到通知的應用程式來說非常有用。  
  
 當查詢的基礎資料變更時，查詢通知可讓您在指定的逾時期間要求通知。 通知的要求會指定通知選項，其中包含服務名稱、訊息文字和伺服器的逾時值。 通知會透過 Service Broker 佇列傳遞，應用程式會輪詢此佇列以查看是否有可用的通知。  
  
 查詢通知選項字串的語法為：  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 例如：  
  
 `service=mySSBService;local database=mydb`  
  
 通知訂閱的存留時間會超過初始化這些訂閱的程序，因為應用程式可以建立通知訂閱，然後再加以結束。 訂閱仍會保持有效，而如果資料在建立訂閱時所指定的逾時期間內變更，就會發生通知。 通知會由執行的查詢、通知選項和訊息文字來識別，並且可藉由將逾時值設定為零而加以取消。  
  
 通知只會傳送一次。 如果要持續接到資料變更的通知，必須在處理過每個通知之後重新執行查詢，以建立新的訂閱。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端應用程式通常會使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [receive](/sql/t-sql/statements/receive-transact-sql)命令，從與通知選項中指定之服務相關聯的佇列讀取通知，以接收通知。  
  
> [!NOTE]  
>  您必須在需要通知的查詢中限定資料表名稱，例如 `dbo.myTable`。 資料表名稱必須使用兩部分的名稱來加以限定。 如果使用三或四部份的名稱，則訂閱無效。  
  
 通知基礎結構是依照 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引進的佇列功能而建立。 一般而言，在伺服器所產生的通知會透過這些佇列傳送，以供稍後處理。  
  
 若要使用查詢通知，伺服器上必須有佇列和服務。 這些項目可以使用類似下列的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 來建立：  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  服務必須使用預先定義的合約 `https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification` (如上所示)。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者支援在資料列集修改時使用取用者通知。 使用者會在資料列集修改的每個階段以及嘗試進行任何變更時收到通知。  
  
> [!NOTE]  
>  使用**ICommand：： Execute**將通知查詢傳遞至伺服器，是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者來訂閱查詢通知的唯一有效方法。  
  
### <a name="the-dbpropset_sqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET 屬性集  
 為了透過 OLE DB 支援查詢通知， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會將下列新屬性新增至 DBPROPSET_SQLSERVERROWSET 屬性集。  
  
|名稱|類型|描述|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|查詢通知要維持使用中的秒數。<br /><br /> 預設值為 432000 秒 (5 天)。 最小值為 1 秒，最大值為 2^31-1 秒。|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|通知的訊息文字。 這是使用者定義的，而且沒有預先定義的格式。<br /><br /> 根據預設，字串是空的。 您可以使用 1-2000 個字元指定訊息。|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|查詢通知選項。 這些是在*名稱* = *值*語法的字串中指定。 使用者負責建立此服務以及從佇列讀取通知。<br /><br /> 預設值是空字串。|  
  
 無論陳述式是以使用者交易或自動認可執行，或者陳述式在其中執行的交易是否已經認可或回復，系統閱永遠都會認可通知訂閱。 伺服器通知會在發生下列任何無效通知條件時觸發：基礎資料或結構描述變更，或達到逾時期限 (視何者為先)。 通知註冊會在觸發之後立刻刪除。 因此在接到通知後，應用程式必須再進行一次訂閱，才能接到進一步的更新。  
  
 其他的連接或執行緒可以檢查目的地佇列是否有通知。 例如：  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 請注意，SELECT * 並不會從佇列刪除項目，但 RECEIVE \* FROM 會這麼做。 如果佇列是空的，這麼做會使伺服器延滯。 如果呼叫時有佇列項目，則這些項目會立刻傳回；否則呼叫會等到佇列項目建立後才進行。  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 如果佇列是空的，這個陳述式會立刻傳回空的結果集；否則會傳回所有的佇列通知。  
  
 如果 SSPROP_QP_NOTIFICATION_MSGTEXT 和 SSPROP_QP_NOTIFICATION_OPTIONS 非 NULL 且不是空的，則每次執行命令時，都會將包含以上定義的三個屬性的查詢通知 TDS 標頭傳送到伺服器。 如果其中任一項為 Null (或是空的)，則該標頭不會傳送且會引發 DB_E_ERRORSOCCURRED (如果這兩個屬性都標示為選擇性的，則會引發 DB_S_ERRORSOCCURRED)，而且狀態值會設定為 DBPROPSTATUS_BADVALUE。 在執行/準備時會進行驗證。 同樣地，當針對 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本連接設定查詢通知屬性時，會引發 DB_S_ERRORSOCCURED。 狀態值在這種情況下是 DBPROPSTATUS_NOTSUPPORTED。  
  
 初始化訂閱並不保證後續的訊息能成功傳遞。 此外，系統也不會對所指定服務名稱的有效性進行檢查。  
  
> [!NOTE]  
>  陳述式的準備永遠都不會初始化訂閱，只有陳述式的執行才會造成初始化，此外使用 OLE DB 核心服務也不會影響查詢通知。  
  
 如需 DBPROPSET_SQLSERVERROWSET 屬性集的詳細資訊，請參閱資料列[集屬性和行為](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式透過將三個新屬性新增至[SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md)和[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)函數，來支援查詢通知：  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
  
 如果 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 和 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 並非 NULL，則每次執行命令時，都會將包含上述定義的三個屬性的查詢通知 TDS 標頭傳送到伺服器。 如果其中任一項為 Null，則不會傳送標頭，而會傳回 SQL_SUCCESS_WITH_INFO。 驗證會在[SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360)函式、 **SqlExecDirect**和**SqlExecute**上進行，而且如果屬性無效，這些會失敗。 同樣地，當針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 版本設定這些查詢通知屬性時，執行會失敗且引發 SQL_SUCCESS_WITH_INFO。  
  
> [!NOTE]  
>  訂閱永遠都不會因為準備陳述式而初始化，但可能會因為執行陳述式而初始化。  
  
## <a name="special-cases-and-restrictions"></a>特殊案例和限制  
 通知不支援下列資料類型：  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
 如果針對傳回任何這些類型的查詢進行通知要求，就會立刻觸發通知，指出不可能進行通知訂閱。  
  
 如果訂閱要求是針對批次或預存程序所建立的，就會針對批次或預存程序內執行的每個陳述式建立個別的訂閱要求。 EXECUTE 陳述式不會註冊通知，不過會將通知要求傳送至執行的命令。 如果它是批次，內容就會套用至執行的陳述式，而且適用上述的相同規則。  
  
 提交在相同資料庫內容下由相同使用者提交之通知的查詢，並具有相同的範本、相同的參數值、相同的通知識別碼，以及現有作用中訂閱的相同傳遞位置，將會更新現有的訂閱，並重設新指定的超時時間。這表示如果要求相同查詢的通知，則只會傳送一則通知。 這適用於批次中重複的查詢，或預存程序中多次呼叫的查詢。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
