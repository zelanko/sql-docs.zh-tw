---
title: 建立連接字串 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
author: rothja
ms.author: jroth
ms.openlocfilehash: b58dc19097d01630fa1ab1c2707e8be379ae83cb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761144"
---
# <a name="creating-a-connection-string"></a>建立連接字串
連接字串是由引數/值組的清單（也就是參數）所組成，並以分號分隔。 例如：  
  
```syntax
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 ADO 或指定的提供者都必須識別所有參數。  
  
 ADO 會辨識連接字串中的下列五個引數。  
  
|引數|描述|  
|--------------|-----------------|  
|*提供者*|指定要用於連接的提供者名稱。|  
|*檔案名稱*|指定包含預設連接資訊的提供者特定檔案（例如保存的資料來源物件）的名稱。|  
|*URL*|將連接字串指定為識別資源（例如檔案或目錄）的絕對 URL。|  
|*遠端提供者*|指定開啟用戶端連接時所要使用的提供者名稱。 （僅限遠端資料服務）。|  
|*遠端伺服器*|指定要在開啟用戶端連接時使用的伺服器路徑名稱。 （僅限遠端資料服務）。|  
  
 其他引數會傳遞至*provider*引數中指定的提供者，而不會由 ADO 進行任何處理。  
  
 HelloData 中的 HelloData 應用程式[：簡單的 ADO 應用程式](../../../ado/guide/data/hellodata-a-simple-ado-application.md)使用了下列連接字串：  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 在此連接字串中，ADO 只會辨識 `"Provider=SQLOLEDB"` 參數，以將 SQL Server 的 Microsoft OLE DB 提供者指定為 ADO 資料來源。 其餘的引數/值組 `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"` 會逐字傳遞給此提供者。 這類參數的類型和有效性是提供者特有的。 如需可在連接字串中傳遞之有效參數的相關資訊，請參閱個別提供者的檔。  
  
 根據 SQL Server 檔的 OLE DB 提供者，您可以將*資料來源*參數和 "Database" 的 "Server" 取代為*初始目錄*參數。 因此，下列連接字串會產生與上方相同的結果：  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
