---
title: 使用 SQLBrowse 連接連接 |微軟文件
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
ms.openlocfilehash: e4d738d394bb3c507f6aa08f736016b51ac4fefb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294658"
---
# <a name="connecting-with-sqlbrowseconnect"></a>使用 SQLDriverConnect 進行連線
**SQLBrowseConnect**,就像**SQLDriverConnect**一樣,使用連接字串。 但是,通過使用**SQLBrowseConnect**,應用程式可以在運行時構造完整的連接字串。 這可以讓應用程式執行兩個動作：  
  
-   構建自己的對話框以提示此資訊,從而保留對其"外觀"的控制。  
  
-   瀏覽系統中，特定驅動程式可使用的資料來源 (可能是透過數個步驟)。 例如，使用者介面可能會先瀏覽網路中的伺服器，然後在選擇伺服器之後，瀏覽伺服器中可由驅動程式存取的資料庫。  
  
 應用程式呼叫**SQLBrowseConnect**並傳遞一個連接字串,稱為*瀏覽請求連接字串,* 指定驅動程式或資料來源。 驅動程式傳回連線字串,是*瀏覽結果連接字串,* 其中包含關鍵字、可能的值(如果關鍵字接受一組離散的值)和使用者友好名稱。 應用程式生成一個對話框,其中包含使用者友好的名稱,並提示使用者輸入值。 然後,它會從這些值產生一個新的瀏覽請求連接字串,並將該字串返回給驅動程式,另一個呼叫**SQLBrowseConnect**。  
  
 由於連接字串是來回傳遞的,因此當應用程式返回舊連接字串時,驅動程式可以通過返回新的連接字串來提供多個級別的流覽。 例如,應用程式首次調用**SQLBrowseConnect**時,驅動程式可能會返回關鍵字以提示使用者輸入伺服器名稱。 當應用程式返回伺服器名稱時,驅動程式可能會返回關鍵字以提示用戶創建資料庫。 應用程式返回資料庫名稱後,瀏覽過程將完成。  
  
 每次**SQLBrowseConnect**傳回一個新的瀏覽結果連接字串時,它都會返回SQL_NEED_DATA作為返回代碼。 這告訴應用程式連接過程不完整。 **在 SQLBrowseConnect**傳回SQL_SUCCESS之前,連接處於「需要資料」狀態,不能用於其他目的,例如設定連接屬性。 應用程式可以通過調用**SQLDisconnect**終止連接瀏覽過程。  
  
 本節包含以下主題。  
  
-   [SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
