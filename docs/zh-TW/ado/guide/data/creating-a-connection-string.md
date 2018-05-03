---
title: 建立的連接字串 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ebe447a23ad88502903e4fa10d9ec502bd4781c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="creating-a-connection-string"></a>建立連接字串
連接字串包含以分號分隔的引數/值組 （也就是 「 參數 」） 清單。 例如：  
  
```  
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 所有參數必須能夠都辨識 ADO 或指定的提供者。  
  
 ADO 會辨識下列五個引數中的連接字串。  
  
|引數|Description|  
|--------------|-----------------|  
|*提供者*|指定要用於連接的提供者的名稱。|  
|*檔案名稱*|指定的提供者特定的檔案 （例如，保存的資料來源物件） 包含預設的連接資訊的名稱。|  
|*URL*|指定的連接字串，以做為識別的資源，例如檔案或目錄的絕對 URL。|  
|*遠端提供者*|指定開啟用戶端連接時使用的提供者的名稱。 （僅限遠端資料服務。）|  
|*遠端伺服器*|指定要開啟的用戶端連接時使用的伺服器的路徑名稱。 （僅限遠端資料服務。）|  
  
 其他引數會傳遞給提供者中名為*提供者*引數，而不需要任何 ADO 所處理。  
  
 HelloData 應用程式中的[HelloData: 簡單的 ADO 應用程式](../../../ado/guide/data/hellodata-a-simple-ado-application.md)使用下列連接字串：  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 在此連接字串中 ADO 只辨識`"Provider=SQLOLEDB"`參數，指定 Microsoft OLE DB Provider for SQL Server 做為 ADO 資料來源。 其餘的引數/值組， `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`，會逐字給此提供者。 類型和這類參數的有效性是特定提供者。 如需有效的連接字串中可傳遞的參數資訊，請參閱個別提供者的文件。  
  
 根據 OLE DB Provider for SQL Server 文件，您可以取代 「 伺服器 」 的*資料來源*參數和 「 資料庫 」 的*初始目錄*參數。 因此，下列連接字串會產生與上面相同的結果：  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
