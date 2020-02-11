---
title: 連接 SQLBrowseConnect |Microsoft Docs
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
ms.openlocfilehash: 04df089b97bf385925c87a98b3f89cdac3ef21e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083128"
---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLDriverConnect 進行連線
**SQLBrowseConnect**（例如**SQLDriverConnect**）會使用連接字串。 不過，藉由使用**SQLBrowseConnect**，應用程式可以在執行時間建立完整的連接字串。 這可以讓應用程式執行兩個動作：  
  
-   建立自己的對話方塊來提示您輸入此資訊，藉此維持對其「外觀與風格」的控制權。  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。 例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 應用程式會呼叫**SQLBrowseConnect** ，並傳遞指定驅動程式或資料來源的連接字串，稱為「*流覽要求連接字串*」。 驅動程式會傳回連接字串，稱為「*流覽結果」連接字串，* 其中包含關鍵字、可能的值（如果關鍵字接受一組離散的值）和使用者易記的名稱。 應用程式會建立一個對話方塊，其中包含使用者易記的名稱，並提示使用者輸入值。 然後，它會從這些值建立新的流覽要求連接字串，並使用**SQLBrowseConnect**的另一個呼叫將它傳回給驅動程式。  
  
 因為連接字串會來回傳遞，所以驅動程式可以在應用程式傳回舊的連接字串時，提供數個層級的流覽。 例如，當應用程式第一次呼叫**SQLBrowseConnect**時，驅動程式可能會傳回關鍵字，以提示使用者輸入伺服器名稱。 當應用程式傳回伺服器名稱時，驅動程式可能會傳回關鍵字來提示使用者輸入資料庫。 流覽進程會在應用程式傳回資料庫名稱後完成。  
  
 每次**SQLBrowseConnect**傳回新的流覽結果連接字串時，它會傳回 SQL_NEED_DATA 做為其傳回碼。 這會告訴應用程式連線進程未完成。 在**SQLBrowseConnect**傳回 SQL_SUCCESS 之前，連接會處於需要資料狀態，而且不能用於其他用途，例如設定連接屬性。 應用程式可以藉由呼叫**SQLDisconnect**來終止連線流覽進程。  
  
 本章節包含下列主題。  
  
-   [SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
