---
title: 建立連接字串 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41732b25c7b2c02f5b6b8a319e057d204a3a3384
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611381"
---
# <a name="creating-a-connection-string"></a>建立連接字串
連接字串是由以分號分隔的引數/值組 （也就是 「 參數 」） 清單所組成。 例如：  
  
```  
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 所有參數必須能夠都辨識 ADO 或指定的提供者。  
  
 ADO 可辨識的連接字串中的下列五個引數。  
  
|引數|描述|  
|--------------|-----------------|  
|*提供者*|指定要用於連線提供者的名稱。|  
|*檔案名稱*|指定提供者特定檔案名稱 （例如，保存的資料來源物件） 包含預設的連接資訊。|  
|*URL*|指定的連接字串做為識別的資源，例如檔案或目錄的絕對 URL。|  
|*遠端提供者*|指定開啟用戶端連接時使用的提供者的名稱。 （僅限遠端資料服務。）|  
|*遠端伺服器*|指定要開啟用戶端連線時所使用的伺服器的路徑名稱。 （僅限遠端資料服務。）|  
  
 其他引數會傳遞給提供者中名為*提供者*引數，而不進行任何處理由 ADO。  
  
 HelloData 應用程式中的[HelloData: 簡易 ADO 應用程式](../../../ado/guide/data/hellodata-a-simple-ado-application.md)使用下列連接字串：  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 在此連接字串中，ADO 會辨識只`"Provider=SQLOLEDB"`參數，指定 Microsoft OLE DB Provider for SQL Server 做為 ADO 資料來源。 其餘的引數/值組， `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`，會逐字給這個提供者。 型別和這類參數的有效性是特定提供者。 如需有效的參數，可在連接字串中傳遞資訊，請參閱個別提供者的文件。  
  
 根據 OLE DB Provider for SQL Server 文件，您可以使用 「 伺服器 」 取代為*資料來源*參數和 「 資料庫 」，如*Initial Catalog*參數。 因此，下列連接字串會產生與上面相同的結果：  
  
```  
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
