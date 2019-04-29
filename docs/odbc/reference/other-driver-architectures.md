---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd051d018cb6f53b8c08110e26bc66910e3ca4c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63045519"
---
# <a name="other-driver-architectures"></a>其他驅動程式架構
有些 ODBC 驅動程式不完全符合先前所述的架構。 這可能是因為驅動程式執行傳統的 ODBC 驅動程式以外的職責，或不是一般意義的驅動程式。  
  
## <a name="driver-as-a-middle-component"></a>驅動程式做為中間的元件  
 ODBC 驅動程式可能位於一個或多個其他的 ODBC 驅動程式與驅動程式管理員。 在中間的驅動程式能夠處理多個資料來源時，它會充當發送器的實際存取資料來源的其他模組的 ODBC 呼叫 （或適當的已翻譯的呼叫）。 在此架構中，在中間的驅動程式所花的驅動程式管理員 」 角色的一些。  
  
 這種驅動程式的另一個範例是 ODBC，後者會攔截並複製 ODBC 驅動程式管理員與驅動程式之間傳送的函式的間諜程式。 此圖層可用來模擬驅動程式或應用程式。 至驅動程式管理員 中，圖層會顯示驅動程式;驅動程式時，圖層會顯示為驅動程式管理員。  
  
## <a name="heterogeneous-join-engines"></a>異質性聯結引擎  
 有些 ODBC 驅動程式會根據執行異質聯結的查詢引擎。 異質性聯結引擎的一個架構中 （請參閱下圖），驅動程式會出現應用程式，但做為應用程式出現到另一個執行個體的驅動程式管理員中的驅動程式。 此驅動程式會處理異質聯結從應用程式，藉由呼叫每個聯結的資料庫驅動程式中個別的 SQL 陳述式。  
  
 ![異質性聯結引擎的架構](../../odbc/reference/media/fig3-4.gif "fig3 4")  
  
 此架構會提供要從不同的資料庫存取資料的應用程式的通用介面。 它可用來擷取中繼資料，例如特殊的資料行 （資料列識別碼） 的相關資訊的常見方式，且可以呼叫來擷取資料字典資訊的通用類別目錄函式。 藉由呼叫 ODBC 函數**SQLStatistics**，比方說，應用程式可以擷取索引資訊的資料表聯結，即使資料表位於兩個不同的資料庫。 查詢處理器不必擔心資料庫儲存中繼資料的方式。  
  
 應用程式也會有標準存取的資料類型。 ODBC 定義特定 DBMS 的資料類型會對應至一般 SQL 資料類型。 應用程式可以呼叫**SQLGetTypeInfo**來擷取有關資料類型不同的資料庫上的資訊。  
  
 當應用程式產生的異質性聯結陳述式時，查詢處理器，在此架構中剖析 SQL 陳述式，並接著會產生個別加入每個資料庫的 SQL 陳述式。 藉由使用每個驅動程式的相關中繼資料，查詢處理器可以判斷最有效率的智慧型聯結。 比方說，如果陳述式聯結兩個資料表與另一個資料庫上的一個資料表的一個資料庫上，查詢處理器都可以加入其他資料庫中資料表的結果之前一個資料庫上聯結兩個資料表。  
  
## <a name="odbc-on-the-server"></a>在伺服器上的 ODBC  
 ODBC 驅動程式可以安裝在伺服器上，以便在任何一系列的用戶端電腦上的應用程式可以使用。 在此架構中 （請參閱下圖），驅動程式管理員和單一的 ODBC 驅動程式安裝在每個用戶端，並在伺服器上安裝其他驅動程式管理員和一系列的 ODBC 驅動程式。 這可讓各種不同的驅動程式使用和維護伺服器上的每個用戶端存取。  
  
 ![在伺服器上的 ODBC 驅動程式的架構](../../odbc/reference/media/fig3-5.gif "FIG3 5")  
  
 這個架構的優點之一是有效的軟體維護和組態。 驅動程式只需要在同一個地方更新： 在伺服器上。 藉由使用系統資料來源，資料來源可以定義用於在伺服器上所有的用戶端。 不需要在用戶端上定義的資料來源。 連接共用可以用來簡化程序的用戶端連接至資料來源。  
  
 用戶端上的驅動程式通常是非常小的驅動程式傳送到伺服器的驅動程式管理員呼叫。 其規模可以明顯地小於功能完整的 ODBC 驅動程式，在伺服器上。 在此架構中，如果伺服器有更多運算能力可以釋放用戶端的資源。 此外，整個系統的安全性與效率皆可透過安裝備份伺服器和執行負載平衡以最佳化伺服器使用。
