---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f8eaebca02ef3987e3613b5dd896e0f7c130086
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938039"
---
# <a name="network-database-access"></a>網路資料庫存取
透過網路存取資料庫需要多個元件，每個都獨立于，而且位於程式設計介面之下。 下列圖例顯示這些元件。  
  
 ![在網路上存取資料庫的元件](../../odbc/reference/media/pr04.gif "pr04")  
  
 每個元件的進一步說明如下：  
  
-   程式**設計介面**如本節稍早所述，程式設計介面包含應用程式所發出的呼叫。 這些介面（內嵌 SQL、SQL 模組和呼叫層級介面）通常是針對每個 DBMS 所特有，不過它們通常是以 ANSI 或 ISO 標準為基礎。  
  
-   **資料流程通訊協定**資料流程通訊協定會描述 DBMS 與其用戶端之間傳輸的資料串流。 例如，通訊協定可能需要第一個位元組來描述資料流程的其餘部分：要執行的 SQL 語句、傳回的錯誤值，或傳回的資料。 然後，資料流程中其餘資料的格式會相依于此旗標。 例如，錯誤資料流程可能會包含旗標、2個位元組的整數錯誤碼、2個位元組的整數錯誤訊息長度和錯誤訊息。  
  
     資料流程通訊協定是一種邏輯通訊協定，與基礎網路所使用的通訊協定無關。 因此，單一資料流程通訊協定通常可以在許多不同的網路上使用。 資料流程通訊協定通常是專屬的，而且已經過優化，可與特定的 DBMS 搭配使用。  
  
-   **處理序間通訊機制**處理序間通訊（IPC）機制是一個程式與另一個進程通訊時所使用的程式。 範例包括具名管道、TCP/IP 通訊端和 DECnet 通訊端。 IPC 機制的選擇受到使用的作業系統和網路所限制。  
  
-   **網路通訊協定**網路通訊協定是用來透過網路傳輸資料流程。 它可以被視為支援 IPC 機制的配量，此機制是用來執行資料流程通訊協定，以及支援基本的網路作業，例如檔案傳輸和列印共用。 網路通訊協定包含 NetBEUI、TCP/IP、DECnet 和 SPX/IPX，而且是每個網路的特定位址。
