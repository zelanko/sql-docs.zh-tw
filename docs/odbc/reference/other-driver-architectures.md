---
title: 其他驅動程式體系結構 |微軟文件
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
ms.openlocfilehash: ae047fe8014b806d3bda8b0513521b4ddda072a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280528"
---
# <a name="other-driver-architectures"></a>其他驅動程式架構
某些 ODBC 驅動程式與前面描述的體系結構不完全一致。 這可能是因為驅動程式執行傳統ODBC驅動程式以外的職責,或者不是正常意義上的驅動程式。  
  
## <a name="driver-as-a-middle-component"></a>驅動程式作為中間元件  
 ODBC 驅動程式可能位於驅動程式管理員和一個或多個其他ODBC驅動程式之間。 當中間的驅動程式能夠處理多個資料來源時,它將充當 ODBC 調用(或適當轉換的呼叫)到實際存取資料來源的其他模組的調度程式。 在此體系結構中,中間的驅動程式承擔了驅動程式管理器的一些角色。  
  
 此類驅動程式的另一個範例是 ODBC 的間諜程式,它攔截和複製在驅動程式管理器和驅動程式之間發送的 ODBC 函數。 此層可用於類比驅動程式或應用程式。 對驅動程式管理器,圖層似乎是驅動程式;對驅動程式,則圖層顯示為驅動程式。對驅動程式,圖層顯示為驅動程式管理器。  
  
## <a name="heterogeneous-join-engines"></a>異構連線引擎  
 某些 ODBC 驅動程式基於用於執行異構聯接的查詢引擎構建。 在異構聯接引擎的一個體系結構中(請參閱下圖),驅動程式在應用程式中顯示為驅動程式,但在驅動程式管理器的另一個實例中顯示為應用程式。 此驅動程式通過在每個聯接資料庫的驅動程序中調用單獨的 SQL 語句來處理來自應用程式的異構聯接。  
  
 ![異質性聯結引擎的架構](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 此體系結構為應用程式提供了一個通用介面,用於從不同的資料庫訪問數據。 它可以使用一種常用方法來檢索元數據,例如有關特殊列(行標識元)的資訊,並且它可以調用通用目錄函數來檢索數據字典資訊。 例如,通過調用 ODBC 函數**SQLStatistics,** 應用程式可以檢索有關要聯接的表上的索引的資訊,即使表位於兩個單獨的資料庫中也是如此。 查詢處理器不必擔心資料庫如何存儲元數據。  
  
 該應用程式還可以對數據類型進行標準訪問。 ODBC 定義特定於 DBMS 的數據類型映射到的常見 SQL 資料類型。 應用程式可以調用**SQLGetTypeInfo**來檢索有關不同資料庫中數據類型的資訊。  
  
 當應用程式生成異構聯接語句時,此體系結構中的查詢處理器解析 SQL 語句,然後為每個要聯接的資料庫生成單獨的 SQL 語句。 通過使用有關每個驅動程式的元數據,查詢處理器可以確定最高效、最智慧的聯接。 例如,如果語句將一個資料庫上的兩個表與另一個資料庫上的一個表聯接,則查詢處理器可以在將結果與另一個資料庫的表聯接之前將一個資料庫上的兩個表聯接在一起。  
  
## <a name="odbc-on-the-server"></a>伺服器上的 ODBC  
 ODBC 驅動程式可以安裝在伺服器上,以便應用程式可以在一系列用戶端計算機上使用它們。 在此架構結構中(請參見下圖),每個用戶端上都安裝了驅動程式管理器和單個ODBC驅動程式,並在伺服器上安裝了另一個驅動程式管理器和一系列ODBC驅動程式。 這允許每個用戶端訪問伺服器上使用和維護的各種驅動程式。  
  
 ![伺服器上 ODBC 驅動程式的架構](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 此體系結構的一個優點是高效的軟體維護和配置。 驅動程式只需在一個位置更新:在伺服器上。 通過使用系統數據源,可以在伺服器上定義數據源,供所有用戶端使用。 不需要在用戶端上定義數據源。 連接池可用於簡化用戶端連接到數據源的過程。  
  
 用戶端上的驅動程式通常是將驅動程式管理器呼叫傳輸到伺服器的非常小的驅動程式。 其佔用空間可以比伺服器上功能齊全的 ODBC 驅動程式小得多。 在此體系結構中,如果伺服器具有更大的計算能力,則可以釋放客戶端資源。 此外,通過安裝備份伺服器和執行負載平衡來優化伺服器使用,可以增強整個系統的效率和安全性。
