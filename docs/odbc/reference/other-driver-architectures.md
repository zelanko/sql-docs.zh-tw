---
description: 其他驅動程式架構
title: 其他驅動程式架構 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44a09eb786abc9f43e25ea105e25e8fdefcdff86
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499661"
---
# <a name="other-driver-architectures"></a>其他驅動程式架構
某些 ODBC 驅動程式並不會嚴格符合先前所述的架構。 這可能是因為驅動程式會執行傳統 ODBC 驅動程式以外的職責，或不是正常的驅動程式。  
  
## <a name="driver-as-a-middle-component"></a>作為中間元件的驅動程式  
 ODBC 驅動程式可能位於驅動程式管理員和一或多個其他 ODBC 驅動程式之間。 當中間的驅動程式能夠使用多個資料來源時，它會作為 ODBC 呼叫的發送器， (或適當轉譯的呼叫) 至實際存取資料來源的其他模組。 在此架構中，中間的驅動程式會採用驅動程式管理員的部分角色。  
  
 這類驅動程式的另一個範例是 ODBC 的 spy 程式，它會攔截和複製在驅動程式管理員與驅動程式之間傳送的 ODBC 函數。 這一層可以用來模擬驅動程式或應用程式。 若為驅動程式管理員，圖層會顯示為驅動程式;若為驅動程式，圖層會顯示為驅動程式管理員。  
  
## <a name="heterogeneous-join-engines"></a>異類聯結引擎  
 某些 ODBC 驅動程式是以查詢引擎為基礎來執行異類聯結。 在異類聯結引擎的一個架構中 (查看下圖) ，驅動程式會以驅動程式的形式出現在應用程式中，但會顯示為驅動程式管理員的另一個實例做為應用程式。 此驅動程式會在每個聯結資料庫的驅動程式中呼叫個別的 SQL 語句，以處理來自應用程式的異類聯結。  
  
 ![異質性聯結引擎的架構](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 此架構提供了一個通用介面，可讓應用程式從不同的資料庫存取資料。 它可以使用常見的方式來取出中繼資料，例如特殊資料行 (資料列識別碼) 的相關資訊，而且可以呼叫一般目錄函數來取出資料字典資訊。 例如，藉由呼叫 ODBC 函數 **SQLStatistics**，應用程式就可以取得要聯結之資料表上的索引相關資訊，即使資料表位於兩個不同的資料庫上也一樣。 查詢處理器不需要擔心資料庫儲存中繼資料的方式。  
  
 應用程式也具有資料類型的標準存取權。 ODBC 會定義 DBMS 特定資料類型所對應的常見 SQL 資料類型。 應用程式可以呼叫 **SQLGetTypeInfo** 來取得不同資料庫的資料類型相關資訊。  
  
 當應用程式產生異類聯結語句時，此架構中的查詢處理器會剖析 SQL 語句，然後針對每個要聯結的資料庫產生個別的 SQL 語句。 藉由使用每個驅動程式的相關中繼資料，查詢處理器可以決定最有效率的智慧型聯結。 例如，如果語句在一個資料庫上聯結兩個數據表，而另一個資料庫上有一個資料表，則查詢處理器可以聯結一個資料庫的兩個數據表，然後將結果與另一個資料庫的資料表聯結。  
  
## <a name="odbc-on-the-server"></a>伺服器上的 ODBC  
 ODBC 驅動程式可以安裝在伺服器上，讓應用程式可以在一系列的用戶端電腦上使用。 在此架構中 (見下圖) ，驅動程式管理員和單一 ODBC 驅動程式會安裝在每個用戶端上，而另一個驅動程式管理員和一系列的 ODBC 驅動程式會安裝在伺服器上。 這可讓每個用戶端存取伺服器上使用和維護的各種驅動程式。  
  
 ![伺服器上 ODBC 驅動程式的架構](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 此架構的其中一個優點是有效率的軟體維護和設定。 驅動程式只需要在單一位置更新：在伺服器上。 藉由使用系統資料來源，可以在伺服器上定義資料來源，以供所有用戶端使用。 資料來源不需要在用戶端上定義。 連接共用可以用來簡化用戶端連接到資料來源的程式。  
  
 用戶端上的驅動程式通常是非常小的驅動程式，可將驅動程式管理員呼叫傳送至伺服器。 它的使用量可能會比伺服器上功能完整的 ODBC 驅動程式明顯小。 在此架構中，如果伺服器有更多的運算能力，就可以釋放用戶端資源。 此外，您可以安裝備份伺服器並執行負載平衡，以優化伺服器的使用，以增強整個系統的效率和安全性。
