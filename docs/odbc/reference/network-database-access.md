---
title: "網路存取資料庫 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5220da346aea15e2dc56224001b0d803c90e0047
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="network-database-access"></a>網路資料庫存取權
透過網路存取資料庫需要多個元件，其中每一個都是獨立的和位於下方的程式設計介面。 下列圖例顯示這些元件。  
  
 ![透過網路存取的資料庫元件](../../odbc/reference/media/pr04.gif "pr04")  
  
 每個元件的進一步描述如下：  
  
-   **程式設計介面**程式設計介面如本節稍早所述，包含應用程式所進行的呼叫。 這些介面 (內嵌 SQL，SQL 模組和介面呼叫層級) 專屬於通常每個 dbms 所特有，但是它們通常根據 ANSI 或 ISO 標準。  
  
-   **資料流通訊協定**資料資料流通訊協定所描述的 DBMS 和其用戶端之間傳輸的資料流。 例如，通訊協定可能需要的第一個位元組，以描述其餘的資料流所包含的內容： SQL 陳述式執行時，傳回的錯誤值，或傳回的資料。 資料流中的其餘部分的格式然後取決於這個旗標。 例如，錯誤資料流可能包含旗標、 2 個位元組的整數錯誤程式碼，2 位元組整數錯誤訊息長度和錯誤訊息。  
  
     資料流通訊協定是邏輯的通訊協定，而且獨立於基礎網路使用的通訊協定。 因此，單一資料流通訊協定通常可以使用不同的網路數目。 資料流通訊協定都通常專屬，且已經過最佳化，使用特定 DBMS。  
  
-   **處理序間通訊機制**的處理序間通訊 (IPC) 機制，是由其中一個處理序通訊與另一個程序。 範例包括具名的管道、 TCP/IP 通訊端和 DECnet 通訊端。 IPC 機制的選擇是由作業系統和所使用的網路限制。  
  
-   **網路通訊協定**網路通訊協定用來透過網路傳輸資料流。 它可以視為支援的 IPC 機制，用來實作資料流通訊協定，以及支援基本的網路作業，例如檔案傳輸及列印共用的配管。 網路通訊協定包括 NetBEUI、 TCP/IP、 DECnet 和 SPX/IPX，以及專屬於每個網路。
