---
title: "連接與 SQLBrowseConnect |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f2f1f3b183810e52f59945b7bc1888421cf48fc6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLBrowseConnect 連接
**SQLBrowseConnect**、 like **SQLDriverConnect**，會使用連接字串。 不過，透過使用**SQLBrowseConnect**，應用程式可以在執行階段建構完整的連接字串。 這可以讓應用程式執行兩個動作：  
  
-   建置自己的對話方塊提示您輸入這項資訊，藉此保持控制其 「 外觀與風格。 」  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。 例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 應用程式會呼叫**SQLBrowseConnect**並傳遞連接字串，又稱為*要求連接字串中，瀏覽*指定驅動程式或資料來源。 驅動程式會傳回連接字串，又稱為*結果連接字串中，瀏覽*包含關鍵字、 可能的值 （如果關鍵字接受一組離散值），以及使用者易記的名稱。 應用程式建置一個對話方塊，以易記的名稱，並提示使用者提供值。 然後建立這些值從新的瀏覽要求連接字串和驅動程式與另一個呼叫會傳回這**SQLBrowseConnect**。  
  
 因為來回傳遞連接字串，此驅動程式可以提供數個層級來傳回新的連接字串，當應用程式會傳回舊瀏覽。 例如，應用程式呼叫第一次**SQLBrowseConnect**，驅動程式可能會傳回關鍵字來提示使用者輸入伺服器名稱。 當應用程式會傳回伺服器名稱時，此驅動程式可能會傳回關鍵字來提示使用者輸入的資料庫。 應用程式會傳回資料庫名稱之後，瀏覽處理序會在完成。  
  
 每次**SQLBrowseConnect**傳回新的瀏覽結果連接字串，它會傳回 SQL_NEED_DATA，做為其傳回的代碼。 這會告訴應用程式的連線程序尚未完成。 直到**SQLBrowseConnect**傳回 SQL_SUCCESS，連接處於需要的資料狀態，無法用於其他用途，例如若要設定的連接屬性。 應用程式可以終止連線瀏覽處理序，藉由呼叫**SQLDisconnect**。  
  
 本章節包含下列主題。  
  
-   [SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)

