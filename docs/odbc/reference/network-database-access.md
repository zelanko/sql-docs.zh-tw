---
title: 網路資料庫訪問 |微軟文件
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
ms.openlocfilehash: 2237c725d6fe3696d1f28d80c09f22183f718de8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295581"
---
# <a name="network-database-access"></a>網路資料庫存取
通過網路訪問資料庫需要許多元件,每個元件都獨立於程式設計介面並位於程式設計介面下面。 下列圖例顯示這些元件。  
  
 ![在網路上存取資料庫的元件](../../odbc/reference/media/pr04.gif "pr04")  
  
 每個元件的進一步說明如下:  
  
-   **程式設計介面**如本節前面所述,程式設計介面包含應用程式發出的調用。 這些介面(嵌入式 SQL、SQL 模組和調用級介面)通常特定於每個 DBMS,儘管它們通常基於 ANSI 或 ISO 標準。  
  
-   **資料流程協定**數據流協定描述在 DBMS 及其客戶端之間傳輸的數據流。 例如,協定可能需要第一個字節來描述流的其餘部分包含的內容:要執行的 SQL 語句、返回的錯誤值或返回的數據。 然後,流中其餘數據的格式將依賴於此標誌。 例如,錯誤流可能包含標誌、2 位元組整數錯誤代碼、2 位元組整數錯誤消息長度和錯誤消息。  
  
     數據流協定是一種邏輯協議,獨立於基礎網路使用的協定。 因此,單個數據流協定通常可以在多個不同的網路上使用。 數據流協定通常是專有的,並已經過優化以與特定的 DBMS 配合使用。  
  
-   **行程間通訊機制**進程間通訊 (IPC) 機制是一個進程與另一個進程通信的過程。 示例包括命名管道、TCP/IP 插槽和 DECnet 套接字。 IPC機制的選擇受到作業系統和網路使用的限制。  
  
-   **網路協定**網路協議用於通過網路傳輸數據流。 它可以被視為支援用於實現資料流協定的 IPC 機制以及支援基本網路操作(如檔案傳輸和列印共用)的管道。 網路協定包括 NetBEUI、TCP/IP、DECnet 和 SPX/IPX,並且特定於每個網路。
