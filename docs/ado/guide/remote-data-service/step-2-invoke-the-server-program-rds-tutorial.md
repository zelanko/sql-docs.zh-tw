---
title: 步驟 2： 叫用伺服器程式 （RDS 教學課程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a2e7b62276234dcf11067395ff2512a8e93af96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800506"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>步驟 2：叫用伺服器程式 (RDS 教學課程)
當您叫用方法，以在用戶端*proxy*，實際的程式，在伺服器上執行的方法。 在此步驟中，您會在伺服器上執行查詢。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 **組件**如果您未使用[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)在本教學課程中，執行此步驟最方便的方式就是使用[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。 **Rds。DataControl**結合上述步驟來建立 proxy，使用此步驟中，發出查詢。  
  
 設定**rds。DataControl**物件[伺服器](../../../ado/reference/rds-api/server-property-rds.md)屬性來識別其中的伺服器程式應該具現化; [Connect](../../../ado/reference/rds-api/connect-property-rds.md)屬性來指定存取資料來源的連接字串和[SQL](../../../ado/reference/rds-api/sql-property.md)屬性來指定查詢命令文字。 接著發出[重新整理](../../../ado/reference/rds-api/refresh-method-rds.md)方法來讓伺服器程式連接到資料來源，擷取指定的查詢，資料列，並傳回**資料錄集**給用戶端的物件。  
  
 本教學課程不會使用**rds。DataControl**，但這是其外觀如果一樣：  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 也不沒有本教學課程以叫用 RDS ADO 物件，但這是其外觀如果有：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **組件 B**執行此步驟的一般方法是叫用**RDSServer.DataFactory**物件[查詢](../../../ado/reference/rds-api/query-method-rds.md)方法。 該方法會接受連接字串，用來連接到資料來源，而命令的文字，這用來指定要從資料來源傳回的資料列。  
  
 本教學課程會使用**DataFactory**物件**查詢**方法：  
  
```  
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [步驟 3： 伺服器取得資料錄集 （RDS 教學課程）](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 教學課程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
