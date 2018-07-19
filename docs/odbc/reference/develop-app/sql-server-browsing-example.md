---
title: 瀏覽範例的 SQL Server |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLBrowseConnect function [ODBC], example
- connecting to data source [ODBC], SqlBrowseConnect
- connecting to driver [ODBC], SQLBrowseConnect
ms.assetid: 6e0d5fd1-ec93-4348-a77a-08f5ba738bc6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 113dd18f5ba6c9d2ff8a74e88a920e71bc145893
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913073"
---
# <a name="sql-server-browsing-example"></a>SQL Server 瀏覽範例
下列範例會示範如何**SQLBrowseConnect**可能用來瀏覽 SQL server 驅動程式可用的連接。 首先，應用程式要求連接控制代碼：  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 下一步，應用程式會呼叫**SQLBrowseConnect**和指定的 SQL Server 驅動程式，使用所傳回的驅動程式描述**SQLDrivers**:  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因為這是第一次呼叫**SQLBrowseConnect**，驅動程式管理員載入 SQL Server 驅動程式，並呼叫驅動程式的**SQLBrowseConnect**它收到來自相同的引數的函式應用程式。  
  
> [!NOTE]  
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定`Trusted_Connection=yes`而不是在連接字串中的使用者識別碼和密碼資訊。  
  
 驅動程式會判斷這是第一次呼叫**SQLBrowseConnect**並傳回連接屬性的第二個層級： 伺服器、 使用者名稱、 密碼、 應用程式名稱和工作站識別碼。 伺服器屬性，它會傳回有效的伺服器名稱的清單。 來自的傳回碼**SQLBrowseConnect**是 SQL_NEED_DATA。 以下是瀏覽結果字串：  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 瀏覽結果字串中的每個關鍵字後面的冒號和等號前面的一或多個字。 這些字是應用程式可用來建置對話方塊中的使用者易記名稱。 **應用程式**和**WSID**關鍵字都會加上星號，表示為選擇性。 **伺服器**， **UID**，和**PWD**關鍵字都會不加上星號，必須為其提供值下, 一步 瀏覽要求字串。 值**伺服器**關鍵字可能是其中一部伺服器所傳回**SQLBrowseConnect**或使用者提供的名稱。  
  
 應用程式會呼叫**SQLBrowseConnect**同樣地，指定綠色的伺服器，以及省略**應用程式**和**WSID**關鍵字和好記的名稱，每個關鍵字後面：  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 驅動程式會嘗試連接到綠色的伺服器。 如果有任何非嚴重錯誤，例如遺漏的關鍵字-值組， **SQLBrowseConnect**傳回 SQL_NEED_DATA，因為發生錯誤之前，會保留在相同的狀態。 應用程式可以呼叫**SQLGetDiagField**或**SQLGetDiagRec**判斷的錯誤。 如果連接成功，驅動程式傳回 SQL_NEED_DATA，並瀏覽結果字串會傳回：  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 這個字串中的屬性是選擇性的因為應用程式可以省略它們。 不過，應用程式必須呼叫**SQLBrowseConnect**一次。 如果省略資料庫名稱和語言選擇應用程式，它會指定空的瀏覽要求字串。 在此範例中，應用程式選擇 pubs 資料庫並呼叫**SQLBrowseConnect**最後一次，省略**語言**關鍵字和之前星號**資料庫**關鍵字：  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 因為**資料庫**屬性是由驅動程式所需的最後一個連接屬性中，瀏覽的程序已完成，應用程式連接到資料來源，以及**SQLBrowseConnect**傳回 SQL_SUCCESS。 **SQLBrowseConnect**也會傳回完整的連接字串，以瀏覽結果字串：  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 驅動程式所傳回的最後一個連接字串不包含使用者易記的名稱之後每個關鍵字，, 也不包含未指定應用程式的選擇性關鍵字。 應用程式可以使用這個字串使用**SQLDriverConnect**重新連接至目前的連接控制代碼上的資料來源 （中斷連接之後），或連接到不同的連接控制代碼上的資料來源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
