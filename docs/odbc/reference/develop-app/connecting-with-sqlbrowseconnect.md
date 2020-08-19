---
description: 使用 SQLDriverConnect 進行連線
title: 使用 SQLBrowseConnect 連接 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7ad54276f54155c68fbdbe984642dda4300a7c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424820"
---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLDriverConnect 進行連線
**SQLBrowseConnect**（例如 **SQLDriverConnect**）會使用連接字串。 不過，藉由使用 **SQLBrowseConnect**，應用程式可以在執行時間建立完整的連接字串。 這可以讓應用程式執行兩個動作：  
  
-   建立自己的對話方塊以提示您輸入此資訊，藉此維持其「外觀與風格」的控制權。  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。 例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 應用程式會呼叫 **SQLBrowseConnect** ，並傳遞指定驅動程式或資料來源的連接字串（稱為「 *流覽要求」連接字串）* 。 驅動程式會傳回連接字串（稱為「 *流覽結果」連接字串* ），其中包含關鍵字、可能的值 (如果關鍵字接受一組離散的值) 和使用者易記名稱。 應用程式會建立一個對話方塊，其中包含使用者易記名稱，並提示使用者輸入值。 然後，它會從這些值建立新的流覽要求連接字串，並使用另一個 **SQLBrowseConnect**呼叫，將此字串傳回至驅動程式。  
  
 因為連接字串會來回傳遞，所以驅動程式可以在應用程式傳回舊的連接字串時，藉由傳回新的連接字串來提供數個層級的流覽。 例如，當應用程式第一次呼叫 **SQLBrowseConnect**時，驅動程式可能會傳回關鍵字以提示使用者提供伺服器名稱。 當應用程式傳回伺服器名稱時，驅動程式可能會傳回關鍵字以提示使用者輸入資料庫。 流覽程式會在應用程式傳回資料庫名稱之後完成。  
  
 每次 **SQLBrowseConnect** 傳回新的流覽結果連接字串時，就會傳回 SQL_NEED_DATA 做為其傳回碼。 這會告訴應用程式連接程式未完成。 除非 **SQLBrowseConnect** 傳回 SQL_SUCCESS，否則連接會處於 [需要資料] 狀態，而且不能用於其他用途，例如設定連接屬性。 應用程式可以藉由呼叫 **SQLDisconnect**來終止連接流覽程式。  
  
 本節包含下列主題。  
  
-   [SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
