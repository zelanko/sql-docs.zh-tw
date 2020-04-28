---
title: 資料長度、緩衝區長度和截斷 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data length [ODBC]
- truncating data [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 2825c6e7-b9ff-42fe-84fc-7fb39728ac5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2e7b8d1e60cd83594509c2ab5cbc24e04546eca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305225"
---
# <a name="data-length-buffer-length-and-truncation"></a>資料長度、緩衝區長度和截斷
*資料長度*是儲存在應用程式資料緩衝區中的資料位元組長度，而不是儲存在資料來源中。 這項區別很重要，因為資料通常會儲存在資料緩衝區中的不同類型，而不是資料來源中。 因此，若要將資料傳送至資料來源，這是轉換成資料來源類型之前的資料位元組長度。 對於從資料來源抓取的資料，這是轉換成資料緩衝區的類型之後，以及在執行任何截斷之前的資料位元組長度。  
  
 如果是固定長度的資料，例如整數或日期結構，資料的位元組長度一定是資料類型的大小。 一般而言，應用程式會配置資料類型大小的資料緩衝區。 如果應用程式佈建較小的緩衝區，則會產生未定義的結果，因為驅動程式會假設資料緩衝區是資料類型的大小，而且不會截斷資料以符合較小的緩衝區。 如果應用程式佈建較大的緩衝區，則絕不會使用多餘的空間。  
  
 對於可變長度的資料（例如字元或二進位資料），請務必辨識資料的位元組長度與緩衝區的位元組長度不同，而且通常會與緩衝區的位元組長度不相同。 這兩個長度的關聯描述于 [[緩衝區](../../../odbc/reference/develop-app/buffers.md)] 區段中。 如果資料的位元組長度大於緩衝區的位元組長度，驅動程式會將提取的資料截斷到緩衝區的位元組長度，並傳回 SQLSTATE 01004 的 SQL_SUCCESS_WITH_INFO （資料已截斷）。 不過，傳回的位元組長度是 untruncated 資料的長度。  
  
 例如，假設應用程式為二進位資料緩衝區配置50個位元組。 如果驅動程式有10個位元組的二進位資料要傳回，則會在緩衝區中傳回這10個位元組。 資料的位元組長度為10，而緩衝區的位元組長度為50。 如果驅動程式有60個位元組的二進位資料要傳回，則會將資料截斷為50個位元組，並傳回緩衝區中的那些位元組，並傳回 SQL_SUCCESS_WITH_INFO。 資料的位元組長度為60（截斷前的長度），而緩衝區的位元組長度仍然是50。  
  
 會針對每個已截斷的資料行建立診斷記錄。 因為驅動程式需要一些時間來建立這些記錄，而讓應用程式處理它們，所以截斷可能會降低效能。 通常，應用程式可以藉由配置足夠的緩衝區來避免這個問題，但在處理長資料時可能無法這麼做。 發生資料截斷時，應用程式有時會配置較大的緩衝區並重新擷取資料;這在所有情況下都是如此。 如果使用**SQLGetData**呼叫來取得資料時發生截斷，應用程式就不需要針對已經傳回的資料呼叫**SQLGetData** ;如需詳細資訊，請參閱[取得長資料](../../../odbc/reference/develop-app/getting-long-data.md)。
