---
title: "驅動程式管理員 &#39; s 角色在連線程序 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 797d3439b378cb5caef62af019352ff6797fdb43
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>驅動程式管理員 &#39; s 角色在連線程序
請記住，應用程式不驅動程式函式會直接呼叫。 相反地，它們呼叫驅動程式管理員函式具有相同名稱和驅動程式管理員呼叫驅動程式函式。 通常，這是幾乎立即。 例如，應用程式呼叫**SQLExecute**驅動程式管理員在驅動程式管理員及完成後一些錯誤檢查，呼叫**SQLExecute**驅動程式中。  
  
 在連線程序會不同。 當應用程式呼叫**SQLAllocHandle** SQL_HANDLE_ENV 並利用 SQL_HANDLE_DBC 的選項，函式會配置控制代碼只有在驅動程式管理員。 驅動程式管理員不會呼叫此函式在驅動程式，因為不知道要呼叫哪一個驅動程式。 同樣地，如果應用程式傳遞未連接的連接控制代碼**SQLSetConnectAttr**或**SQLGetConnectAttr**，只有驅動程式管理員會執行函式。 它會儲存或取得其連接的屬性值處理，並傳回 SQLSTATE 08003 （未開啟連接） 時取得值的屬性尚未設定，供 ODBC 未定義預設值。  
  
 當應用程式呼叫**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**，驅動程式管理員會先判斷要使用哪一個驅動程式。 然後它會檢查以判斷驅動程式目前是否已載入連接上：  
  
-   如果在連接上載入沒有驅動程式時，驅動程式管理員會檢查指定的驅動程式是否已載入的相同環境中的另一個連接上。 如果不是，驅動程式管理員會載入驅動程式在連接並呼叫**SQLAllocHandle** SQL_HANDLE_ENV 選項與驅動程式中。  
  
     驅動程式管理員接著呼叫**SQLAllocHandle**中利用 SQL_HANDLE_DBC 選項與驅動程式，不論它是剛載入。 如果應用程式設定任何連接屬性，驅動程式管理員呼叫**SQLSetConnectAttr**在驅動程式; 如果發生錯誤時，驅動程式管理員連接函數會傳回 SQLSTATE IM006 (驅動程式的**SQLSetConnectAttr**失敗)。 最後，驅動程式管理員在驅動程式中呼叫連線函式。  
  
-   如果指定的驅動程式已載入連接上，驅動程式管理員會驅動程式中呼叫連線函式。 在此情況下，驅動程式必須確定所有連接屬性連接上的都維持其目前的設定。  
  
-   如果在連接上載入不同的驅動程式時，驅動程式管理員呼叫**SQLFreeHandle**驅動程式來釋放連接中。 如果沒有其他使用驅動程式的連接，驅動程式管理員呼叫**SQLFreeHandle**驅動程式來釋放環境中載入和卸載驅動程式。 驅動程式管理員接著執行時載入驅動程式不在此連接上為相同的作業。  
  
 驅動程式管理員將會在鎖定環境控制代碼 (*henv*) 之前呼叫的驅動程式**SQLAllocHandle**和**SQLFreeHandle**時*HandleType*設**利用 SQL_HANDLE_DBC**。  
  
 當應用程式呼叫**SQLDisconnect**，驅動程式管理員呼叫**SQLDisconnect**驅動程式中。 不過，它會保留以防應用程式重新連線到驅動程式載入的驅動程式。 當應用程式呼叫**SQLFreeHandle**利用 SQL_HANDLE_DBC 選項時，驅動程式管理員呼叫**SQLFreeHandle**驅動程式中。 如果驅動程式不是由任何其他連接，驅動程式管理員會呼叫**SQLFreeHandle** SQL_HANDLE_ENV 與驅動程式選項和卸載驅動程式。
