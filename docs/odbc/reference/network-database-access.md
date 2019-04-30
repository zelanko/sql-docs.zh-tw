---
title: 網路資料庫存取權 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ff13d2e46377b0d29c9bbc8e8ad1705dedc048b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63272893"
---
# <a name="network-database-access"></a>網路資料庫存取
透過網路存取的資料庫需要多個元件，其中每一個都是獨立的且下方的程式設計介面。 下列圖例顯示這些元件。  
  
 ![在網路上存取資料庫的元件](../../odbc/reference/media/pr04.gif "pr04")  
  
 每個元件的進一步說明如下：  
  
-   **程式設計介面**的程式設計介面如本節稍早所述，包含應用程式所進行的呼叫。 這些介面 (內嵌 SQL，SQL 模組，以及呼叫層級介面) 特有通常每個 DBMS，雖然它們通常以 ANSI 或 ISO 標準為基礎。  
  
-   **Data Stream 通訊協定**資料流通訊協定所描述的 DBMS 和其用戶端之間傳輸的資料流。 例如，通訊協定可能會需要來描述資料流的其餘部分所包含的第一個位元組： 要執行，傳回的錯誤值，或傳回資料的 SQL 陳述式。 這個旗標則會取決於資料流中的其餘部分的格式。 比方說，旗標、 2 位元整數的錯誤程式碼、 2 個位元組整數錯誤訊息長度和一則錯誤訊息，可能包含錯誤資料流。  
  
     資料流通訊協定是邏輯的通訊協定，並且獨立於基礎網路所使用的通訊協定。 因此，單一資料流通訊協定通常可以使用不同的網路數目。 資料流通訊協定是通常是專用的並已最佳化來處理特定 DBMS。  
  
-   **處理序間通訊機制**的處理序間通訊 (IPC) 機制是由其中一個處理序通訊與另一個程序。 範例包括具名的管道、 TCP/IP 通訊端，以及 DECnet 通訊端。 IPC 機制的選擇會受到作業系統和所使用的網路。  
  
-   **網路通訊協定**網路通訊協定用來透過網路傳輸的資料流。 它可以被視為支援的 IPC 機制，用來實作資料流通訊協定，以及支援基本的網路作業，例如檔案傳輸及列印共用的配管。 網路通訊協定包括 NetBEUI、 TCP/IP、 DECnet 和 SPX/IPX，並且專屬於每個網路。
