---
title: 驅動程式管理員&#39;s 的連線程序中的角色 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f69ae2b8c00f062d3650606de071a4d07eefab4e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607246"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>驅動程式管理員&#39;s 的連線程序中的角色
請記住，應用程式不驅動程式函式會直接呼叫。 相反地，它們呼叫具有相同名稱的驅動程式管理員函式，而驅動程式管理員呼叫的驅動程式函式。 通常，這幾乎會立即發生。 例如，應用程式會呼叫**SQLExecute**驅動程式管理員在驅動程式管理員和一些錯誤檢查後，呼叫**SQLExecute**驅動程式中。  
  
 連線處理方式不同。 當應用程式呼叫**SQLAllocHandle** SQL_HANDLE_ENV 並利用 SQL_HANDLE_DBC 之選項的函式會配置控制代碼只有在驅動程式管理員。 驅動程式管理員不會呼叫此函式，驅動程式中的，因為它不知道要呼叫哪一個驅動程式。 同樣地，如果應用程式會將未連線至連接的控制代碼**SQLSetConnectAttr**或是**SQLGetConnectAttr**，只有驅動程式管理員會執行函式。 它會儲存或取得屬性值，從其連線的處理，並傳回 SQLSTATE 08003 （未開啟連接） 時取得值的屬性尚未設定，以及哪些 odbc 不會定義預設值。  
  
 當應用程式呼叫**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**，驅動程式管理員首先會決定要使用哪一個驅動程式。 然後它會檢查以判斷是否連接目前載入的驅動程式：  
  
-   如果在連接上不載入任何驅動程式時，驅動程式管理員會檢查指定的驅動程式是否已載入的相同環境中的另一個連接上。 如果不是，驅動程式管理員載入的驅動程式連接並呼叫**SQLAllocHandle** SQL_HANDLE_ENV 選項與驅動程式中。  
  
     驅動程式管理員接著會呼叫**SQLAllocHandle**中利用 SQL_HANDLE_DBC 選項與驅動程式時，是否是剛載入。 如果應用程式設定任何連接屬性，驅動程式管理員會呼叫**SQLSetConnectAttr**驅動程式; 中發生錯誤時，驅動程式管理員的連線函式會傳回 SQLSTATE IM006 (駕**SQLSetConnectAttr**失敗)。 最後，驅動程式管理員會呼叫驅動程式中的連線函式。  
  
-   如果在連接上載入指定的驅動程式時，驅動程式管理員會驅動程式中呼叫只連接函式。 在此情況下，驅動程式必須確定所有的連接屬性，在此連接上維持其目前的設定。  
  
-   如果在連接上載入不同的驅動程式時，驅動程式管理員會呼叫**SQLFreeHandle**來釋放連接驅動程式中。 如果沒有其他使用驅動程式的連接，驅動程式管理員會呼叫**SQLFreeHandle**驅動程式來釋放環境中載入和卸載該驅動程式。 驅動程式管理員接著會執行為時載入驅動程式不在此連接上相同的作業。  
  
 驅動程式管理員將會在鎖定環境控制代碼 (*henv*) 呼叫的驅動程式之前先**SQLAllocHandle**並**SQLFreeHandle**當*HandleType*設定為**利用 SQL_HANDLE_DBC**。  
  
 當應用程式呼叫**SQLDisconnect**，此驅動程式管理員會呼叫**SQLDisconnect**驅動程式中。 不過，它會保留萬一應用程式重新連接到驅動程式載入的驅動程式。 當應用程式呼叫**SQLFreeHandle**利用 SQL_HANDLE_DBC 選項時，驅動程式管理員會呼叫**SQLFreeHandle**驅動程式中。 如果驅動程式未使用任何其他連接，驅動程式管理員接著會呼叫**SQLFreeHandle** SQL_HANDLE_ENV 與驅動程式選項，然後卸載該驅動程式。
