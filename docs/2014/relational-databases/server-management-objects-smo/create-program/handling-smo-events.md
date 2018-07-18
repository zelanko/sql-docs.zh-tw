---
title: 處理 SMO 事件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e74a05e025f474737130f1faeb61f2647d8e69bd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212988"
---
# <a name="handling-smo-events"></a>處理 SMO 事件
  有些伺服器事件類型可以藉由事件處理常式和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件進行訂閱。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 中的許多執行個體類別，都會在伺服器上發生特定動作時觸發事件。  
  
 這些事件可以藉由設定事件處理常式及訂閱相關事件，以程式設計的方式來處理。 這種事件處理類型是暫時性的，因為當 SMO 用戶端程式結束時會將訂閱全數移除。  
  
## <a name="connectioncontext-event-handling"></a>ConnectionContext 事件處理  
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件支援數種事件類型。 事件屬性必須設定為具有適當事件處理常式的執行個體，而事件處理常式物件則必須定義為可以處理事件的受保護函數。  
  
## <a name="event-subscription"></a>事件訂閱  
 您可藉由下列步驟來處理事件：撰寫事件處理常式類別、建立其執行個體、將事件處理常式指派給父物件，然後再訂閱事件。  
  
 您必須撰寫事件處理常式類別，才能處理事件。 事件處理常式類別可以包含一個以上的事件處理常式函數，而且必須加以安裝，才能處理事件。 事件處理常式函式會接收來自事件的相關資訊*ServerEventNotificatificationArgs*可以用來報告該事件的相關資訊的參數。  
  
 資料庫和伺服器可以處理的事件類型會列在<xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet>類別和<xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>類別。  
  
## <a name="example"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>在 Visual Basic 中註冊事件處理常式及訂閱事件處理  
 此程式碼範例示範如何設定事件處理常式，以及如何訂閱資料庫事件。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEvents1](SMO How to#SMO_VBEvents1)]  -->  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>在 Visual C# 中註冊事件處理常式及訂閱事件處理  
 此程式碼範例示範如何設定事件處理常式，以及如何訂閱資料庫事件。  
  
```  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  
