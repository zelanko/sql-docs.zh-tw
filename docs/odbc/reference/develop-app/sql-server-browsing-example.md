---
title: SQL Server 流覽範例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f3a7568c0849844526ef5f172bcecc0a5857268
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114333"
---
# <a name="sql-server-browsing-example"></a>SQL Server 瀏覽範例
下列範例示範如何使用**SQLBrowseConnect**來流覽驅動程式可用的連接，以進行 SQL Server。 首先，應用程式會要求連接控制碼：  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 接下來，應用程式會呼叫**SQLBrowseConnect** ，並使用**SQLDrivers**所傳回的驅動程式描述來指定 SQL Server 驅動程式：  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因為這是第一次呼叫**SQLBrowseConnect**，驅動程式管理員會載入 SQL Server 驅動程式，並使用從應用程式收到的相同引數來呼叫驅動程式的**SQLBrowseConnect**函式。  
  
> [!NOTE]  
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在`Trusted_Connection=yes`連接字串中指定而不是使用者識別碼和密碼資訊。  
  
 驅動程式會判斷這是第一次呼叫**SQLBrowseConnect** ，並傳回第二層的連接屬性：伺服器、使用者名稱、密碼、應用程式名稱和工作站識別碼。 針對伺服器屬性，它會傳回有效伺服器名稱的清單。 來自**SQLBrowseConnect**的傳回碼為 SQL_NEED_DATA。 以下是流覽結果字串：  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 流覽結果字串中的每個關鍵字後面會接著一個冒號，以及一個或多個在等號之前的文字。 這些字是使用者易記的名稱，可讓應用程式用來建立對話方塊。 **應用程式**和**WSID**關鍵字的前面會加上星號，這表示它們是選擇性的。 **SERVER**、 **UID**和**PWD**關鍵字的前面不加星號;您必須在下一個流覽要求字串中提供值給它們。 **SERVER**關鍵字的值可以是**SQLBrowseConnect**所傳回的其中一部伺服器，或是使用者提供的名稱。  
  
 應用程式會再次呼叫**SQLBrowseConnect** ，並指定綠色伺服器，並省略**應用程式**和**WSID**關鍵字，以及每個關鍵字之後的使用者易記名稱：  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 驅動程式會嘗試連接到綠色伺服器。 如果發生任何非嚴重錯誤，例如遺漏的關鍵字-值組，則**SQLBrowseConnect**會傳回 SQL_NEED_DATA，並維持在錯誤之前的相同狀態。 應用程式可以呼叫**SQLGetDiagField**或**SQLGetDiagRec**來判斷錯誤。 如果連接成功，驅動程式會傳回 SQL_NEED_DATA 並傳回流覽結果字串：  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 因為此字串中的屬性是選擇性的，所以應用程式可以省略它們。 不過，應用程式必須再次呼叫**SQLBrowseConnect** 。 如果應用程式選擇省略資料庫名稱和語言，它會指定空白的流覽要求字串。 在此範例中，應用程式會選擇 pubs 資料庫，並在最後一次呼叫**SQLBrowseConnect** ，並省略**database**關鍵字之前的**LANGUAGE**關鍵字和星號：  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因為**資料庫**屬性是驅動程式所需的最後一個連接屬性，所以流覽程式已完成，應用程式會連接到資料來源，而**SQLBrowseConnect**會傳回 SQL_SUCCESS。 **SQLBrowseConnect**也會傳回完整的連接字串作為流覽結果字串：  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 驅動程式傳回的最後一個連接字串不包含每個關鍵字後面的易記名稱，也不包含應用程式未指定的選擇性關鍵字。 應用程式可以使用此字串搭配**SQLDriverConnect** ，在目前的連接控制碼（中斷連接之後）重新連接到資料來源，或連接到不同連接控制碼上的資料來源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
