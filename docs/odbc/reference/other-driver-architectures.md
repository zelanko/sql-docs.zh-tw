---
title: 其他驅動程式架構 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52b51847dee6dbe59a7bb4495e0739d2ee08c005
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="other-driver-architectures"></a>其他驅動程式架構
有些 ODBC 驅動程式不完全符合先前所述的架構。 這可能是因為驅動程式執行責任以外的傳統的 ODBC 驅動程式，或不正常的意義上的驅動程式。  
  
## <a name="driver-as-a-middle-component"></a>驅動程式，做為中間的元件  
 ODBC 驅動程式可能位於驅動程式管理員與一或多個其他 ODBC 驅動程式。 在中間的驅動程式能夠使用多個資料來源時，它會充當發送器的實際存取資料來源的其他模組呼叫 ODBC （或適當地翻譯的呼叫）。 在這種架構，中間的驅動程式所花費的部份的驅動程式管理員 」 角色。  
  
 這類的驅動程式的另一個範例是 ODBC，後者會攔截，並將複製的 ODBC 驅動程式管理員與驅動程式之間傳送的函式的間諜程式。 此圖層可以用來模擬驅動程式或應用程式。 至驅動程式管理員，圖層會顯示驅動程式。驅動程式時，圖層會呈現為驅動程式管理員。  
  
## <a name="heterogeneous-join-engines"></a>異質性聯結引擎  
 有些 ODBC 驅動程式是建置在執行異質聯結的查詢引擎。 在一個異質性聯結引擎的架構 （請參閱下圖），驅動程式會對應用程式顯示為驅動程式但會與另一個執行個體的驅動程式管理員中顯示為應用程式。 此驅動程式會處理應用程式從異質聯結藉由呼叫個別的 SQL 陳述式中的驅動程式，針對每個聯結的資料庫。  
  
 ![異質性聯結引擎的架構](../../odbc/reference/media/fig3-4.gif "fig3 4")  
  
 此架構會提供要從不同的資料庫存取資料的應用程式的通用介面。 它可以使用擷取中繼資料，例如特殊的資料行 （資料列識別碼） 的相關資訊的常見方式，它可以呼叫來擷取資料字典資訊的通用類別目錄函式。 藉由呼叫 ODBC 函數**SQLStatistics**，比方說，應用程式可以擷取索引資訊的資料表聯結，即使資料表位於兩個不同的資料庫。 查詢處理器不必擔心資料庫將中繼資料的儲存方式。  
  
 應用程式也會有資料類型的標準權限。 ODBC 定義特定 DBMS 的資料類型會對應至一般 SQL 資料類型。 應用程式可以呼叫**SQLGetTypeInfo**擷取在不同的資料庫資料類型的相關資訊。  
  
 當應用程式產生異質性聯結陳述式時，查詢處理器在這種架構會剖析 SQL 陳述式，並接著會產生個別的 SQL 陳述式，針對要加入的每個資料庫。 藉由使用每個驅動程式的相關中繼資料，查詢處理器可以決定最有效率、 智慧型聯結。 比方說，如果陳述式聯結兩個資料表與另一個資料庫上的一個資料表的一個資料庫上，查詢處理器可以聯結兩個資料表一個資料庫之後，再將結果與另一個資料庫的資料表。  
  
## <a name="odbc-on-the-server"></a>在伺服器上的 ODBC  
 ODBC 驅動程式可以安裝在伺服器上，以便在任何一系列的用戶端電腦上的應用程式可以使用。 在這種架構 （請參閱下圖），驅動程式管理員和單一的 ODBC 驅動程式安裝在每個用戶端，並在伺服器上安裝其他驅動程式管理員及一系列的 ODBC 驅動程式。 這可讓各種不同的驅動程式使用，以及在伺服器上維護的每個用戶端存取。  
  
 ![在伺服器上的 ODBC 驅動程式的架構](../../odbc/reference/media/fig3-5.gif "FIG3 5")  
  
 這個架構的其中一個優點是有效的軟體維護和組態。 驅動程式只需要在一個地方更新： 伺服器上。 藉由使用系統資料來源，資料來源可以定義使用的伺服器上的所有用戶端。 不需要在用戶端上定義的資料來源。 連接共用可以用來簡化用戶端連接到資料來源之程序。  
  
 用戶端上的驅動程式通常是非常小的驅動程式傳送到伺服器的驅動程式管理員呼叫。 其可以是遠小於完整運作的伺服器上的 ODBC 驅動程式。 在這種架構，如果伺服器有更多計算能力可以釋放用戶端的資源。 此外，整個系統的安全性與效率可以藉此獲得增強安裝備份伺服器和執行負載平衡最佳化伺服器使用。
