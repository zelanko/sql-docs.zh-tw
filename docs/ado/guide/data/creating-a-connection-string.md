---
description: 建立連接字串
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
ms.openlocfilehash: f544805336fdea586fac5697b3abde009dc6f7ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453620"
---
# <a name="creating-a-connection-string"></a>建立連接字串
連接字串是由引數/值組的清單所組成 (也就是) 的參數，以分號分隔。 例如：  
  
```syntax
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 所有參數都必須由 ADO 或指定的提供者辨識。  
  
 ADO 會辨識連接字串中的下列五個引數。  
  
|引數|描述|  
|--------------|-----------------|  
|*提供者*|指定連接所要使用之提供者的名稱。|  
|*檔案名稱*|指定提供者特定檔案的名稱 (例如，保存的資料來源物件) 包含預設的連接資訊。|  
|*URL*|將連接字串指定為識別資源的絕對 URL，例如檔案或目錄。|  
|*遠端提供者*|指定開啟用戶端連接時要使用的提供者名稱。  (僅限遠端資料服務。 ) |  
|*遠端伺服器*|指定開啟用戶端連接時要使用之伺服器的路徑名稱。  (僅限遠端資料服務。 ) |  
  
 其他引數會傳遞給 *提供者* 引數中所指定的提供者，而不會由 ADO 處理。  
  
 HelloData 中的 HelloData 應用程式 [：簡單的 ADO 應用程式](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 使用下列連接字串：  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 在此連接字串中，ADO 只會辨識 `"Provider=SQLOLEDB"` 參數，以指定 Microsoft OLE DB Provider for SQL Server 作為 ADO 資料來源。 其餘的引數/值組 `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"` 會逐字傳遞給這個提供者。 這類參數的類型和有效性是提供者特有的。 如需可在連接字串中傳遞之有效參數的詳細資訊，請參閱個別提供者的檔。  
  
 根據 SQL Server 檔的 OLE DB 提供者，您可以將 "Server" 取代為 *資料來源* 參數，並將 "Database" 取代為 *初始目錄* 參數。 因此，下列連接字串會產生與上述相同的結果：  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
