---
title: SQL 伺服器瀏覽範例 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b15aa8e3d573660a312fceb5b9100a41f0384d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301979"
---
# <a name="sql-server-browsing-example"></a>SQL Server 瀏覽範例
下面的範例展示如何使用**SQLBrowseConnect**來流覽 SQL Server 驅動程式可用的連接。 首先,應用程式請求連接句柄:  
  
```  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
```  
  
 接下來,應用程式呼叫**SQLBrowseConnect**並指定 SQL Server 驅動程式,使用**SQLDriver**傳回的驅動程式說明 :  
  
```  
SQLBrowseConnect(hdbc, "DRIVER={SQL Server};", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 由於這是第一次調用**SQLBrowseConnect,** 驅動程式管理器載入 SQL Server 驅動程式,並且使用從應用程式接收的相同參數調用驅動程式的**SQLBrowse Connect**函數。  
  
> [!NOTE]  
>  如果要連接到支援 Windows 身份驗證的資料來源提供者,則應在連接字串`Trusted_Connection=yes`中指定 而不是使用者 ID 和密碼資訊。  
  
 驅動程式確定這是對**SQLBrowseConnect**的第一次調用,並返回第二級連接屬性:伺服器、使用者名、密碼、應用程式名稱和工作站 ID。 對於伺服器屬性,它返回有效伺服器名稱的清單。 **SQLBrowseConnect**的返回代碼SQL_NEED_DATA。 下面是瀏覽結果字串:  
  
```  
"SERVER:Server={red,blue,green,yellow};UID:Login ID=?;PWD:Password=?;  
   *APP:AppName=?;*WSID:WorkStation ID=?;"  
```  
  
 流覽結果字串中的每個關鍵字後面跟一個冒號和等於符號前的一個或多個單詞。 這些單詞是應用程式可用於生成對話框的使用者友好名稱。 **APP**和**WSID**關鍵字由星號預綴,這意味著它們是可選的。 **伺服器****、UID**和**PWD**關鍵字不由星號預綴;必須在下一個流覽請求字串中為它們提供值。 **SERVER**關鍵字的值可能是**SQLBrowseConnect**傳回的伺服器之一或使用者提供的名稱。  
  
 應用程式再次呼叫**SQLBrowseConnect,** 指定綠色伺服器,並省略**APP**和**WSID**關鍵字以及每個關鍵字後的使用者友好名稱:  
  
```  
SQLBrowseConnect(hdbc, "SERVER=green;UID=Smith;PWD=Sesame;", SQL_NTS,  
                  BrowseResult, sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 驅動程式嘗試連接到綠色伺服器。 如果存在任何非致命錯誤(如缺少關鍵字值對 **),SQLBrowseConnect**將返回SQL_NEED_DATA並保留與錯誤之前相同的狀態。 應用程式可以調用**SQLGetDiagField**或**SQLGetDiagRec**來確定錯誤。 如果連線成功,驅動程式將傳回SQL_NEED_DATA並傳回瀏覽結果字串:  
  
```  
"*DATABASE:Database={master,model,pubs,tempdb};  
   *LANGUAGE:Language={us_english,Franais};"  
```  
  
 由於此字串中的屬性是可選的,因此應用程式可以省略它們。 但是,應用程式必須再次調用**SQLBrowseConnect。** 如果應用程式選擇省略資料庫名稱和語言,它將指定一個空流覽請求字串。 這個範例中,應用程式選擇 pubs 資料庫並呼叫**SQLBrowseConnect**進行最後一次,省略**了語言**關鍵字和**DATABASE**關鍵字前的星號:  
  
```  
SQLBrowseConnect(hdbc, "DATABASE=pubs;", SQL_NTS, BrowseResult,  
                  sizeof(BrowseResult), &BrowseResultLen);  
```  
  
 由於**DATABASE**屬性是驅動程式所需的最終連接屬性,因此流覽過程已完成,應用程式已連接到數據源 **,SQLBrowseConnect**返回SQL_SUCCESS。 **SQLBrowseConnect**還會將完整的連接字串作為瀏覽結果字串傳回:  
  
```  
"DSN=MySQLServer;SERVER=green;UID=Smith;PWD=Sesame;DATABASE=pubs;"  
```  
  
 驅動程式返回的最終連接字串不包含每個關鍵字之後的使用者友好名稱,也不包含應用程式未指定的可選關鍵字。 應用程式可以使用此字串與**SQLDriverConnect**重新連接到目前連接句柄上的數據來源(斷開連接後),或連接到其他連接句柄上的數據源。 例如：  
  
```  
SQLDriverConnect(hdbc, hwnd, BrowseResult, SQL_NTS, ConnStrOut,  
                  sizeof(ConnStrOut), &ConnStrOutLen, SQL_DRIVER_NOPROMPT);  
```
