---
title: 使用 sqldriverconnect 進行連接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1cd42e6704bc5168b1eb20841100fc279a66ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042764"
---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLDriverConnect 進行連線
**SQLBrowseConnect**，例如**SQLDriverConnect**，會使用連接字串。 不過，藉由使用**SQLBrowseConnect**，應用程式可以在執行階段建構完整的連接字串。 這可以讓應用程式執行兩個動作：  
  
-   建置自己的對話方塊提示您輸入這項資訊，藉此保持控制其 「 外觀與風格。 」  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。 例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 應用程式會呼叫**SQLBrowseConnect** ，並傳遞連接字串，又稱為*瀏覽要求的連接字串，* ，指定驅動程式或資料來源。 驅動程式會傳回連接字串，稱為*瀏覽結果的連接字串，* 包含關鍵字、 可能的值 （如果關鍵字會接受一組離散值），以及使用者易記的名稱。 應用程式建置對話方塊，以易記的名稱，並提示使用者提供值。 然後建置這些值從新的瀏覽要求連接字串，並傳回此驅動程式，再呼叫一次**SQLBrowseConnect**。  
  
 因為連接字串會來回傳遞，此驅動程式可以提供數個層級來傳回新的連接字串，當應用程式會傳回舊瀏覽。 比方說，第一次應用程式呼叫**SQLBrowseConnect**，驅動程式可能會傳回關鍵字，以提示使用者輸入伺服器名稱。 當應用程式傳回的伺服器名稱時，驅動程式可能會傳回關鍵字，以提示使用者輸入的資料庫。 應用程式會傳回資料庫名稱之後，瀏覽的程序會完成。  
  
 每次**SQLBrowseConnect**傳回新的瀏覽結果連接字串，它會傳回 SQL_NEED_DATA，為其傳回的程式碼。 這會告訴應用程式在連線程序未完成。 直到**SQLBrowseConnect**傳回 SQL_SUCCESS，連接是在需要的資料狀態，並無法用於其他用途，例如若要設定的連接屬性。 應用程式可以終止連線瀏覽程序，藉由呼叫**SQLDisconnect**。  
  
 本章節包含下列主題。  
  
-   [SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
