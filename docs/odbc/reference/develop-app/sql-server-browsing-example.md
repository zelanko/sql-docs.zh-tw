---
title: 瀏覽範例的 SQL Server |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f8dc57d738c1d5726d2208b930c5d4fadcd93b39
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149309"
---
# <a name="sql-server-browsing-example"></a>SQL Server 瀏覽範例
下列範例示範如何**SQLBrowseConnect**可能會用來瀏覽 SQL Server 隨附的驅動程式的連線。 首先，應用程式會要求在連接控制代碼：  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 接下來，應用程式會呼叫**SQLBrowseConnect** ，並指定 SQL Server 驅動程式，使用所傳回的驅動程式說明**SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因為這是第一次呼叫**SQLBrowseConnect**，驅動程式管理員載入 SQL Server 驅動程式，並呼叫駕**SQLBrowseConnect**搭配來自相同的引數的函式應用程式。  
  
> [!NOTE]  
>  如果您要連接到資料來源提供者支援 Windows 驗證，您應該指定`Trusted_Connection=yes`而不是在連接字串中的使用者識別碼和密碼資訊。  
  
 驅動程式可讓您判斷這是第一次呼叫**SQLBrowseConnect** ，並傳回連接屬性的第二個層級： 伺服器、 使用者名稱、 密碼、 應用程式名稱和工作站識別碼。 伺服器屬性，它會傳回一份有效的伺服器名稱。 傳回碼**SQLBrowseConnect**是 SQL_NEED_DATA。 以下是瀏覽結果字串：  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 瀏覽結果字串中的每個關鍵字後面的冒號和等號前面的一或多個字。 這些字的應用程式可用來建置 對話方塊中的使用者易記名稱。 **應用程式**並**WSID**關鍵字都會加上星號，也就是選擇性。 **伺服器**， **UID**，並**PWD**關鍵字不會加上星號，必須為它們提供值下, 一步 瀏覽要求字串中。 值**伺服器**關鍵字可能會傳回伺服器的其中一個**SQLBrowseConnect**或使用者提供的名稱。  
  
 應用程式會呼叫**SQLBrowseConnect**同樣地，指定綠色的伺服器，以及省略**應用程式**並**WSID**關鍵字和使用者易記的名稱之後每個關鍵字,：  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 驅動程式會嘗試連線到綠色的伺服器。 如果有任何非嚴重錯誤，例如遺漏的關鍵字-值組， **SQLBrowseConnect**會傳回 SQL_NEED_DATA，因為發生錯誤之前，會保留在相同的狀態。 應用程式可以呼叫**SQLGetDiagField**或是**SQLGetDiagRec**來判斷錯誤。 如果連線成功，驅動程式會傳回 SQL_NEED_DATA，並傳回瀏覽的結果字串：  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 這個字串中的屬性是選擇性的因為應用程式可以省略它們。 不過，應用程式必須呼叫**SQLBrowseConnect**一次。 如果省略資料庫名稱和語言選擇應用程式，它會指定空的瀏覽要求的字串。 在此範例中，應用程式選擇 pubs 資料庫，然後呼叫**SQLBrowseConnect**最終的時間，並省略**語言**關鍵字和星號之前**資料庫**關鍵字：  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因為**資料庫**屬性是驅動程式所需的最後一個連接屬性，瀏覽程序已完成，應用程式已連線到資料來源，以及**SQLBrowseConnect**會傳回 SQL_SUCCESS。 **SQLBrowseConnect**也會傳回完整的連接字串，以瀏覽結果字串：  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 驅動程式所傳回的最後一個連接字串不包含使用者易記的名稱之後每個關鍵字，, 也不會包含未指定應用程式的選擇性關鍵字。 應用程式可以使用此字串**SQLDriverConnect** （之後中斷連接） 重新連線到目前的連接控制代碼上的資料來源，或連接到不同的連接控制代碼上的資料來源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
