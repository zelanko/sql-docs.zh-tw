---
description: 網路資料庫存取
title: 網路資料庫存取 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 025959072b7ebadc96fd1d1a628bdfaf5d449940
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461320"
---
# <a name="network-database-access"></a>網路資料庫存取
跨網路存取資料庫需要一些元件，其中每個元件都是獨立的，而且位於程式設計介面底下。 下列圖例顯示這些元件。  
  
 ![在網路上存取資料庫的元件](../../odbc/reference/media/pr04.gif "pr04")  
  
 每個元件的進一步描述如下：  
  
-   程式**設計介面**如本節稍早所述，程式設計介面包含應用程式所進行的呼叫。 這些介面 (內嵌 SQL、SQL 模組和呼叫層級介面) 一般都是針對每個 DBMS 所特有，不過這些介面通常是以 ANSI 或 ISO 標準為基礎。  
  
-   **資料流程通訊協定** 資料流程通訊協定描述 DBMS 與其用戶端之間傳輸的資料串流。 例如，通訊協定可能需要第一個位元組來描述資料流程其餘部分所包含的內容：要執行的 SQL 語句、傳回的錯誤值或傳回的資料。 資料流程中其餘資料的格式會視此旗標而定。 例如，錯誤資料流程可能包含旗標、2位元組整數錯誤碼、2位元組整數錯誤訊息長度，以及錯誤訊息。  
  
     資料流程通訊協定是一種邏輯通訊協定，與基礎網路所使用的通訊協定無關。 因此，單一資料流程通訊協定通常可以用於許多不同的網路上。 資料流程通訊協定通常是專屬的，而且已經過優化，可搭配特定的 DBMS 使用。  
  
-   **處理序間通訊機制** 處理序間通訊 (IPC) 機制是一個進程與另一個進程進行通訊的程式。 範例包括具名管道、TCP/IP 通訊端，以及 DECnet 通訊端。 IPC 機制的選項受限於所使用的作業系統和網路。  
  
-   **網路通訊協定** 網路通訊協定是用來透過網路傳輸資料流程。 它可以被視為支援 IPC 機制的配量，以用來執行資料流程通訊協定，以及支援基本的網路作業，例如檔案傳輸和列印共用。 網路通訊協定包含 NetBEUI、TCP/IP、DECnet 和 SPX/IPX，而且是每個網路專用的。
