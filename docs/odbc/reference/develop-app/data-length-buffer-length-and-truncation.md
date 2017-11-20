---
title: "資料長度，緩衝區長度和截斷 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 616dc403fdd23f3233bde4a5db19dd58b6d94cf1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-length-buffer-length-and-truncation"></a>資料長度，緩衝區長度和截斷
*資料長度*資料的位元組長度，會儲存在應用程式的資料緩衝區，不是它會儲存在資料來源。 此差異很重要的因為資料通常會儲存在資料來源中比資料緩衝區中的不同類型。 因此對於傳送至資料來源的資料，這是之前轉換成資料來源的類型資料的位元組長度。 從資料來源擷取資料，這可以是資料的位元組長度的資料緩衝區的型別以及之前完成任何截斷的轉換後。  
  
 固定長度的資料，例如整數或日期結構，對於資料的位元組長度一律是資料類型的大小。 一般情況下，應用程式配置資料緩衝區大小的資料類型。 如果應用程式會配置較小的緩衝區，因為驅動程式會假設資料緩衝區的資料類型的大小並不會截斷以配合較小的緩衝區中的資料結果便未定義。 如果應用程式會配置較大的緩衝區，絕不會使用額外的空間。  
  
 可變長度的資料，例如字元或二進位資料時，務必辨識資料的位元組長度不同，且通常不同緩衝區的位元組長度。 這些兩個長度關聯述[緩衝區](../../../odbc/reference/develop-app/buffers.md)> 一節。 如果資料的位元組長度大於緩衝區的位元組長度，驅動程式會截斷提取的緩衝區的位元組長度的資料，並會傳回 SQL_SUCCESS_WITH_INFO sqlstate 01004 （資料已截斷）。 不過，傳回的位元組長度會是未截斷的資料長度。  
  
 例如，假設應用程式配置 50 個位元組的二進位資料緩衝區。 如果驅動程式有 10 個位元組的二進位資料傳回時，它會傳回緩衝區中的 10 個位元組。 資料的位元組長度為 10，和緩衝區的位元組長度為 50。 如果驅動程式有 60 個位元組，要傳回的二進位資料，它會截斷為 50 個位元組的資料、 在緩衝區傳回那些位元組和傳回 SQL_SUCCESS_WITH_INFO。 資料的位元組長度是 60 （之前截斷長度），而且緩衝區的位元組長度仍然是 50。  
  
 診斷記錄會建立每個資料行，會被截斷。 若要建立這些記錄驅動程式和應用程式處理，花時間，因為截斷可能會降低效能。 通常，應用程式可以避免這個問題配置夠大的緩衝區，雖然這可能無法使用 long 資料時。 資料截斷發生時，應用程式的有時配置較大的緩衝區和提取資料。這不是在所有情況下，則為 true。 截斷發生時取得的資料呼叫**SQLGetData**，應用程式不需要呼叫**SQLGetData**已傳回的資料; 如需詳細資訊，請參閱[使用者入門Long 資料](../../../odbc/reference/develop-app/getting-long-data.md)。

