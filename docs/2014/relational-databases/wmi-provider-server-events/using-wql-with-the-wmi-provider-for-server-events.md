---
title: 伺服器事件的 WMI 提供者使用 WQL |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 18c4b6448438ebb8c95f999569d51edfecf04206
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375820"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>搭配伺服器事件的 WMI 提供者使用 WQL
  管理應用程式可藉由發出 WMI 查詢語言 (WQL) 陳述式，使用 WMI Provider for Server Events 來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 WQL 是結構化查詢語言 (SQL) 的簡化子集，具有一些 WMI 特定的延伸模組。 在使用 WQL 時，應用程式會針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特定執行個體、資料庫或資料庫物件 (目前唯一支援的物件是佇列) 來擷取事件類型。 伺服器事件的 WMI 提供者會將查詢轉譯為資料庫範圍或物件範圍的事件通知，或在目標資料庫中建立的事件通知**主要**資料庫的伺服器範圍的事件通知。  
  
 例如，請看下列的 WQL 查詢：  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS WHERE DatabaseName = 'AdventureWorks'  
```  
  
 WMI 提供者會嘗試從此查詢在目標伺服器上產生此事件通知的相等項目：  
  
```  
USE AdventureWorks ;  
GO  
  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE   
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',  
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 WQL 查詢的 `FROM` 子句中的引數 (`DDL_DATABASE_LEVEL_EVENTS`) 可以是能在其上建立事件通知的任何有效事件。 `SELECT` 和 `WHERE` 子句中的引數可以指定與事件或其上層事件相關的任何事件屬性。 如需有效事件和事件屬性的清單，請參閱 <<c0> [ 事件通知 (Database Engine)](https://technet.microsoft.com/library/ms182602.aspx)。  
  
 下列 WQL 語法會由 WMI Provider for Server Events 明確支援。 也可以指定其他的 WQL 語法，但該語法並非此提供者所專屬，而會改由其他的 WMI 主機服務進行剖析。 如需有關 WMI 查詢語言的詳細資訊，請參閱 Microsoft Developer Network (MSDN) 上的 WQL 文件集。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition  
```  
  
## <a name="arguments"></a>引數  
 *event_property*  
 這是事件的屬性。 範例包括 `PostTime`、`SPID` 和 `LoginName`。 查閱中所列每個事件[伺服器事件類別和屬性的 WMI 提供者](wmi-provider-for-server-events-classes-and-properties.md)以判斷保存的屬性。 例如，DDL_DATABASE_LEVEL_EVENTS 事件會保存 `DatabaseName` 和 `UserName` 屬性。 它也會從其上層事件繼承 `SQLInstance`、`LoginName`、`PostTime`、`SPID` 和 `ComputerName` 屬性。  
  
 **,** *...n*  
 指出*event_property*可以查詢許多次，並以逗號分隔。  
  
 \*  
 指定要查詢與事件相關聯的所有屬性。  
  
 *event_type*  
 這是任何可針對其而建立事件通知的事件。 如需可用事件的清單，請參閱 <<c0> [ 伺服器事件類別和屬性的 WMI 提供者](https://technet.microsoft.com/library/ms186449.aspx)。 請注意，*事件型別*名稱會對應到相同*event_type* | *event_group*可指定當您手動建立事件通知使用 CREATE EVENT NOTIFICATION。 範例*事件類型*包含 CREATE_TABLE、 LOCK_DEADLOCK、 DDL_USER_EVENTS 和 TRC_DATABASE。  
  
> [!NOTE]  
>  執行類似 DDL 作業的系統預存程序也可以引發事件通知。 請測試事件通知以判斷它們對執行之系統預存程序的回應。 例如，CREATE TYPE 陳述式及**sp_addtype**預存程序都會引發在 CREATE_TYPE 事件建立的事件通知。 不過， **sp_rename**預存程序不會引發任何事件通知。 如需詳細資訊，請參閱 <<c0> [ DDL 事件](../triggers/ddl-events.md)。  
  
 *where_condition*  
 是 WHERE 子句查詢述詞組成*event_property*名稱和邏輯和比較運算子。 *Where_condition*決定目標資料庫中對應的事件通知已註冊的範圍。 它也可以做為篩選器，以特定的結構描述或從中查詢的物件為目標*event_type。* 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。  
  
 只有 `=` 運算子可以搭配 `DatabaseName`、`SchemaName` 和 `ObjectName` 使用。 其他運算式無法搭配這些事件屬性使用。  
  
## <a name="remarks"></a>備註  
 *Where_condition*語法決定下列伺服器事件的 WMI 提供者：  
  
-   由此提供者會嘗試擷取指定的範圍*event_type*： 伺服器層級、 資料庫層級或物件層級 （目前支援的唯一物件是佇列）。 這個範圍最終會判斷在目標資料庫中所建立之事件通知的類型。 這個程序稱為事件通知註冊。  
  
-   可以其上註冊之資料庫、結構描述和物件 (視何者適當)。  
  
 WMI Provider for Server Events 會使用由下而上 (Bottom-Up)、最先合適 (First-Fit) 演算法，針對基礎 EVENT NOTIFICATION 產生最小的可能範圍。 此種演算法會嘗試將伺服器上的內部活動以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和 WMI 主機處理序之間的網路傳輸量降至最低。 提供者會檢查*event_type* FROM 子句和 WHERE 子句中，在條件中指定，並嘗試使用最少的可能範圍註冊基礎的事件通知。 如果提供者不能以最窄的範圍註冊，就會嘗試以連續的較高範圍註冊，直到註冊終於成功為止。 如果在達到最高的範圍 (伺服器層級) 時仍舊失敗，就會對取用者傳回錯誤。  
  
 例如，如果資料庫名稱 =**'** AdventureWorks **'** 在 WHERE 子句中，提供者會嘗試註冊事件通知中的指定[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫。 如果 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫存在，而且呼叫用戶端具有在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中建立事件通知的必要權限，註冊作業就會成功， 否則系統會嘗試在伺服器層級註冊事件通知。 如果 WMI 用戶端擁有必要的權限，註冊就會成功。 不過，在此種情況下，在建立 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫之前，不會對用戶端傳回事件。  
  
 *Where_condition*也可以做為篩選，將此外限制至特定的資料庫、 結構描述或物件查詢。 例如，請看下列的 WQL 查詢：  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 依註冊程序的結果，這個 WQL 查詢可能會註冊於資料庫或伺服器層級。 不過，即使此查詢註冊於伺服器層級，提供者最終仍會篩選出不適用於 `ALTER_TABLE` 資料表的任何 `AdventureWorks.Sales.SalesOrderDetail` 事件。 換言之，提供者只會傳回在該特定資料表上所發生之 `ALTER_TABLE` 事件的屬性。  
  
 如果指定了 `DatabaseName='AW1'` OR `DatabaseName='AW2'` 之類的複合運算式，則會嘗試以伺服器範圍註冊單一的事件通知，而不會註冊兩個個別的事件通知。 如果呼叫用戶端擁有權限，註冊就會成功。  
  
 如果`SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'`都指定在`WHERE`子句中，嘗試以註冊事件通知，直接在物件上的`Z`結構描述中`X`。 如果用戶端擁有權限，註冊就會成功。 請注意，目前物件層級事件支援只能在佇列上，並只為 QUEUE_ACTIVATION *event_type*。  
  
 請注意，並非所有事件都可以在任何的特定範圍上查詢。 例如，在追蹤事件 (例如 Lock_Deadlock) 或追蹤事件群組 (例如 TRC_LOCKS) 上的 WQL 查詢都只能在伺服器層級註冊。 同樣地，CREATE_ENDPOINT 事件和 DDL_ENDPOINT_EVENTS 事件群組也只能在伺服器層級註冊。 如需有關註冊事件適用範圍的詳細資訊，請參閱 <<c0> [ 設計事件通知](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx)。 嘗試登錄 WQL 查詢其*event_type*只能註冊在伺服器層級一定會在伺服器層級。 如果 WMI 用戶端擁有權限，註冊就會成功。 否則，就會對用戶端傳回錯誤。 不過在某些情況下，您仍可以根據與事件相對應的屬性，使用 WHERE 子句做為伺服器層級事件的篩選器。 例如，許多追蹤事件都具有 `DatabaseName` 屬性，可在 WHERE 子句中用來當做篩選器。  
  
 伺服器範圍的事件通知建立在**主要**資料庫，並可以藉由查詢中繼資料[sys.server_event_notifications](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql)目錄檢視。  
  
 資料庫範圍或物件範圍的事件通知會在指定的資料庫中建立，並可以藉由查詢中繼資料[sys.event_notifications](/sql/relational-databases/system-catalog-views/sys-event-notifications-transact-sql)目錄檢視。 (必須將相對應的資料庫名稱當做目錄檢視的前置詞)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>A. 查詢伺服器範圍的事件  
 下列 WQL 查詢會針對任何發生於 `SERVER_MEMORY_CHANGE` 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 追蹤事件，擷取所有的事件屬性。  
  
```  
SELECT * FROM SERVER_MEMORY_CHANGE  
```  
  
### <a name="b-querying-for-events-at-the-database-scope"></a>B. 查詢資料庫範圍的事件  
 下列 WQL 查詢會針對任何發生於 `AdventureWorks` 資料庫且存在於 `DDL_DATABASE_LEVEL_EVENTS` 事件群組下方的事件，擷取特定的事件屬性。  
  
```  
SELECT SPID, SQLInstance, DatabaseName FROM DDL_DATABASE_LEVEL_EVENTS   
WHERE DatabaseName = 'AdventureWorks'   
```  
  
### <a name="c-querying-for-events-at-the-database-scope-filtering-by-schema-and-object"></a>C. 以結構描述和物件進行篩選，查詢資料庫範圍的事件  
 下列查詢會針對任何發生於 `ALTER_TABLE` 資料表的 `AdventureWorks.Sales.SalesOrderDetail` 事件，擷取所有的事件屬性。  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
## <a name="see-also"></a>另請參閱  
 [WMI 事件提供者伺服器概念](https://technet.microsoft.com/library/ms180560.aspx)   
 [事件通知 (Database Engine)](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
