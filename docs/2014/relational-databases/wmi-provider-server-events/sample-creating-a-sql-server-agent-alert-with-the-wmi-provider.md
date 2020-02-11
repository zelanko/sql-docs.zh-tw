---
title: 範例：使用伺服器事件的 WMI 提供者來建立 SQL Server Agent 警示 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SQL Server Agent [WMI]
- WMI Provider for Server Events, samples
- sample applications [WMI]
ms.assetid: d44811c7-cd46-4017-b284-c863ca088e8f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a793c6ee6e1f6e168ca2a957b84b1ba4a1d2a453
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68195840"
---
# <a name="sample-creating-a-sql-server-agent-alert-by-using-the-wmi-provider-for-server-events"></a>範例：使用伺服器事件的 WMI 提供者建立 SQL Server Agent 警示
  使用 WMI 事件提供者的常見方式為建立回應特定事件的 SQL Server Agent 警示。 下列範例顯示一個簡單的警示，可將 XML 死結圖形事件儲存在資料表中，以便稍後進行分析。 SQL Server Agent 會提交 WQL 要求、接收 WMI 事件，以及執行工作來回應事件。 請注意，雖然在處理通知訊息時包含數個 Service Broker 物件，但是 WMI 事件提供者會處理建立與管理這些物件的詳細資料。  
  
## <a name="example"></a>範例  
 首先，在 `AdventureWorks` 資料庫中建立一個資料表來容納死結圖形事件。 此資料表包含兩個資料行：`AlertTime` 資料行容納警示執行的時間，而 `DeadlockGraph` 資料行容納其中包含死結圖形的 XML 文件。  
  
 接著，建立警示。 指令碼會先建立警示將執行的工作、將作業步驟加入到工作中，然後將工作目標瞄準為目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 然後，指令碼會建立警示。  
  
 作業步驟會抓取 WMI 事件實例的**TextData**屬性，並將該值插入**DeadlockEvents**資料表的**DeadlockGraph**資料行中。 請注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會以隱含的方式，將字串轉換為 XML 格式。 作業步驟會使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 子系統，因此，作業步驟不會指定 Proxy。  
  
 每當記錄死結圖形追蹤事件時，警示就會執行作業。 對於 WMI 警示，SQL Server Agent 會使用指定的命名空間和 WQL 陳述式來建立通知查詢。 SQL Server Agent 會針對此警示監視本機電腦上的預設執行個體。 WQL 陳述式會要求預設執行個體中的任何 `DEADLOCK_GRAPH` 事件。 若要變更警示所監視的執行個體，將警示的執行個體名稱取代為 `MSSQLSERVER` 中的 `@wmi_namespace`。  
  
> [!NOTE]  
>  如需接收 WMI 事件的 SQL Server Agent [!INCLUDE[ssSB](../../includes/sssb-md.md)] ，必須在**msdb**和[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]中啟用。  
  
```  
USE AdventureWorks ;  
GO  
  
IF OBJECT_ID('DeadlockEvents', 'U') IS NOT NULL  
BEGIN  
    DROP TABLE DeadlockEvents ;  
END ;  
GO  
  
CREATE TABLE DeadlockEvents  
    (AlertTime DATETIME, DeadlockGraph XML) ;  
GO  
-- Add a job for the alert to run.  
  
EXEC  msdb.dbo.sp_add_job @job_name=N'Capture Deadlock Graph',   
    @enabled=1,   
    @description=N'Job for responding to DEADLOCK_GRAPH events' ;  
GO  
  
-- Add a jobstep that inserts the current time and the deadlock graph into  
-- the DeadlockEvents table.  
  
EXEC msdb.dbo.sp_add_jobstep  
    @job_name = N'Capture Deadlock Graph',  
    @step_name=N'Insert graph into LogEvents',  
    @step_id=1,   
    @on_success_action=1,   
    @on_fail_action=2,   
    @subsystem=N'TSQL',   
    @command= N'INSERT INTO DeadlockEvents  
                (AlertTime, DeadlockGraph)  
                VALUES (getdate(), N''$(ESCAPE_SQUOTE(WMI(TextData)))'')',  
    @database_name=N'AdventureWorks' ;  
GO  
  
-- Set the job server for the job to the current instance of SQL Server.  
  
EXEC msdb.dbo.sp_add_jobserver @job_name = N'Capture Deadlock Graph' ;  
GO  
  
-- Add an alert that responds to all DEADLOCK_GRAPH events for  
-- the default instance. To monitor deadlocks for a different instance,  
-- change MSSQLSERVER to the name of the instance.  
  
EXEC msdb.dbo.sp_add_alert @name=N'Respond to DEADLOCK_GRAPH',   
@wmi_namespace=N'\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER',   
    @wmi_query=N'SELECT * FROM DEADLOCK_GRAPH',   
    @job_name='Capture Deadlock Graph' ;  
GO  
```  
  
## <a name="testing-the-sample"></a>測試範例  
 若要查看作業執行，請先誘發死結。 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，開啟兩個 **[SQL 查詢**] 索引標籤，並將兩個查詢連接到相同的實例。 在其中一個查詢索引標籤中執行下列指令碼。 這個指令碼會產生一個結果集並完成。  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 在第二個 [查詢] 索引標籤中執行下列腳本。此腳本會產生一個結果集，然後封鎖，等待取得上`Production.Product`的鎖定。  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 在第一個 [查詢] 索引標籤中執行下列腳本。此腳本會封鎖，等待取得上`Production.Location`的鎖定。 短暫的逾時之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會選擇此指令碼或範例中的指令碼，做為死結的犧牲者，然後結束交易。  
  
```  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
```  
  
 誘發死結之後稍等一陣子，讓 SQL Server Agent 啟動警示並執行作業。 執行下列指令碼來檢查 `DeadlockEvents` 資料表的內容：  
  
```  
SELECT * FROM DeadlockEvents ;  
GO  
```  
  
 
  `DeadlockGraph` 資料行應該包含顯示死結圖形事件所有屬性的 XML 文件。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器事件的 WMI 提供者概念](wmi-provider-for-server-events-concepts.md)  
  
  
