---
title: 驅動程式管理員在連線進程中&#39;s 角色 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0227a4063573cb05ecaa9434605ba35f2811bd06
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305799"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>驅動程式管理員在連線進程中&#39;s 角色
請記住，應用程式不會直接呼叫驅動程式函式。 相反地，它們會以相同名稱呼叫驅動程式管理員功能，而驅動程式管理員會呼叫驅動程式函式。 通常，這幾乎會立即發生。 例如，應用程式會在驅動程式管理員中呼叫**SQLExecute** ，而在幾次錯誤檢查之後，驅動程式管理員會呼叫驅動程式中的**SQLExecute** 。  
  
 連接程式不同。 當應用程式使用 SQL_HANDLE_ENV 和 SQL_HANDLE_DBC 選項呼叫**SQLAllocHandle**時，函數只會在驅動程式管理員中配置控制碼。 驅動程式管理員不會在驅動程式中呼叫此函式，因為它不知道要呼叫哪一個驅動程式。 同樣地，如果應用程式將未連線連線的控制碼傳遞給**SQLSetConnectAttr**或**SQLGetConnectAttr**，則只有驅動程式管理員會執行函數。 它會儲存或取得其連接控制碼的屬性值，並在取得尚未設定之屬性的值，且 ODBC 未定義預設值的情況下，傳回 SQLSTATE 08003 （連接未開啟）。  
  
 當應用程式呼叫**SQLConnect**、 **SQLDriverConnect**或**SQLBrowseConnect**時，驅動程式管理員會先決定要使用哪一個驅動程式。 然後，它會檢查以判斷連接上目前是否已載入驅動程式：  
  
-   如果連線上沒有載入驅動程式，驅動程式管理員會檢查指定的驅動程式是否已載入至相同環境中的另一個連接。 如果沒有，驅動程式管理員會在連接上載入驅動程式，並使用 SQL_HANDLE_ENV 選項來呼叫驅動程式中的**SQLAllocHandle** 。  
  
     然後，驅動程式管理員會使用 SQL_HANDLE_DBC 選項來呼叫驅動程式中的**SQLAllocHandle** ，不論它是否剛載入。 如果應用程式設定了任何連接屬性，驅動程式管理員就會呼叫驅動程式中的**SQLSetConnectAttr** ;如果發生錯誤，驅動程式管理員的連線功能會傳回 SQLSTATE IM006 （驅動程式的**SQLSetConnectAttr**失敗）。 最後，驅動程式管理員會呼叫驅動程式中的連接功能。  
  
-   如果指定的驅動程式是在連接上載入，驅動程式管理員就只會呼叫驅動程式中的連接功能。 在這種情況下，驅動程式必須確定連接上的所有連接屬性都維持其目前的設定。  
  
-   如果在連接上載入不同的驅動程式，驅動程式管理員會呼叫驅動程式中的**SQLFreeHandle**來釋放連線。 如果沒有其他使用驅動程式的連線，驅動程式管理員會呼叫驅動程式中的**SQLFreeHandle** ，以釋放環境並卸載驅動程式。 然後，驅動程式管理員會執行與連接上未載入驅動程式時相同的作業。  
  
 當*HandleType*設定為**SQL_HANDLE_DBC**時，驅動程式管理員會先鎖定環境控制碼（*henv*），再呼叫驅動程式的**SQLAllocHandle**和**SQLFreeHandle** 。  
  
 當應用程式呼叫**SQLDisconnect**時，驅動程式管理員會呼叫驅動程式中的**SQLDisconnect** 。 不過，如果應用程式重新連接到驅動程式，它會讓驅動程式保持載入。 當應用程式使用 SQL_HANDLE_DBC 選項呼叫**SQLFreeHandle**時，驅動程式管理員會呼叫驅動程式中的**SQLFreeHandle** 。 如果其他連線未使用此驅動程式，驅動程式管理員就會使用 SQL_HANDLE_ENV 選項來呼叫驅動程式中的**SQLFreeHandle** ，並卸載驅動程式。
