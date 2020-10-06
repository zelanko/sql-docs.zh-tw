---
description: 步驟 2：叫用伺服器程式 (RDS 教學課程)
title: 步驟2：叫用伺服器程式 (RDS 教學課程) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: rothja
ms.author: jroth
ms.openlocfilehash: a9238fa208a5ce415986fee05045dc7ea34e0d67
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722999"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>步驟 2：叫用伺服器程式 (RDS 教學課程)
當您在用戶端 *proxy*上叫用方法時，伺服器上的實際程式會執行方法。 在此步驟中，您將在伺服器上執行查詢。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
 **部分 A** 如果您未在本教學課程中使用 [RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) ，執行此步驟最方便的方式就是使用 [RDS。DataControl](../../reference/rds-api/datacontrol-object-rds.md) 物件。 **RDS。DataControl**結合了先前建立 proxy 的步驟，此步驟會發出查詢。  
  
 設定 **RDS。DataControl** 物件 [伺服器](../../reference/rds-api/server-property-rds.md) 屬性，用來識別伺服器程式應該具現化的位置; [連接](../../reference/rds-api/connect-property-rds.md) 屬性，可指定用來存取資料來源的連接字串;和 [SQL](../../reference/rds-api/sql-property.md) 屬性，以指定查詢命令文字。 然後發出 [Refresh](../../reference/rds-api/refresh-method-rds.md) 方法，使伺服器程式連接到資料來源、取出查詢所指定的資料列，並將 **記錄集** 物件傳回至用戶端。  
  
 本教學課程不會使用 **RDS。DataControl**，但這看起來像這樣：  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 本教學課程也會叫用具有 ADO 物件的 RDS，但這是它的外觀：  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **B 部分** 執行此步驟的一般方法是叫用 **RDSServer. DataFactory** 物件 [查詢](../../reference/rds-api/query-method-rds.md) 方法。 該方法會使用連接字串（用來連接到資料來源）和命令文字（用來指定要從資料來源傳回的資料列）。  
  
 本教學課程使用 **DataFactory** 物件 **查詢** 方法：  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [步驟3：伺服器取得記錄集 (RDS 教學課程) ](./step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](./rds-tutorial-vbscript.md)