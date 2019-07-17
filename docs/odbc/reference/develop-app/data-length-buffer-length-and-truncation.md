---
title: 資料長度、 緩衝區長度和截斷 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8586157237db1158587e3c39f1320b78d8251fb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081473"
---
# <a name="data-length-buffer-length-and-truncation"></a>資料長度、緩衝區長度和截斷
*的資料長度*是資料的位元組長度，因為它會儲存在應用程式的資料緩衝區，不如它會儲存在資料來源。 這項區別很重要的因為資料通常儲存在不同的類型，比在資料來源中資料緩衝區中。 針對傳送至資料來源的資料，這是之前轉換成資料來源的類型資料的位元組長度。 從資料來源擷取的資料，這可以是資料的位元組長度轉換成資料緩衝區的型別和任何截斷完成之前後。  
  
 固定長度的資料，例如整數或日期結構，對於資料的位元組長度一律是資料類型的大小。 一般情況下，應用程式配置資料緩衝區大小的資料類型。 如果應用程式配置較小的緩衝區，結果是未定義因為驅動程式會假設資料緩衝區的資料類型大小的作業，而且不會截斷以配合較小的緩衝區的資料。 如果應用程式配置較大的緩衝區，絕不會使用額外的空間。  
  
 對於可變長度的資料，例如字元或二進位資料，請務必辨識資料的位元組長度會不同，且通常不同於緩衝區的位元組長度。 這些兩個長度之關聯性所述[緩衝區](../../../odbc/reference/develop-app/buffers.md)一節。 如果資料的位元組長度大於緩衝區的位元組長度，驅動程式會截斷至緩衝區的位元組長度的擷取的資料，並傳回 SQL_SUCCESS_WITH_INFO 含有 SQLSTATE 01004 （資料已截斷）。 不過，傳回的位元組長度會是未截斷的資料長度。  
  
 例如，假設應用程式配置 50 個位元組的二進位資料緩衝區。 如果驅動程式會有 10 個位元組的二進位資料傳回，它會傳回緩衝區中的這些 10 個位元組。 資料的位元組長度為 10，並將緩衝區的位元組長度為 50。 驅動程式是否要傳回的二進位資料的 60 個位元組，它會截斷為 50 個位元組的資料、 在緩衝區中，會傳回那些位元組並傳回 SQL_SUCCESS_WITH_INFO。 資料的位元組長度為 60 （之前截斷長度），並將緩衝區的位元組長度仍是 50。  
  
 診斷記錄會建立每個資料行，會被截斷。 因為需要一段時間來建立這些記錄驅動程式和處理這些應用程式，截斷可能會降低效能。 通常，應用程式可以避免這個問題配置夠大的緩衝區，雖然這可能不可行時使用長的資料。 資料截斷發生時，應用程式的有時配置較大的緩衝區和重新擷取資料;這不是在所有情況下，則為 true。 如果截斷時發生取得資料，透過呼叫**SQLGetData**，應用程式不需要呼叫**SQLGetData**已傳回的資料; 如需詳細資訊，請參閱[開始Long 資料](../../../odbc/reference/develop-app/getting-long-data.md)。
