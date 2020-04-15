---
title: 數據長度、緩衝區長度和截斷 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305225"
---
# <a name="data-length-buffer-length-and-truncation"></a>資料長度、緩衝區長度和截斷
*數據長度*是數據存儲在應用程式的數據緩衝區中的位元組長度,而不是存儲在數據源中的位元組長度。 這種區別很重要,因為數據通常存儲在數據緩衝區中的不同類型,而不是數據存儲中。 因此,對於發送到數據源的數據,這是數據轉換為數據源類型之前的位元組長度。 對於從數據源檢索的數據,這是轉換為數據緩衝區類型后以及完成任何截斷之前數據的位元組長度。  
  
 對於固定長度數據(如整數或日期結構),數據的位元組長度始終為資料類型的大小。 通常,應用程式分配的數據緩衝區的大小是數據類型的大小。 如果應用程式分配了較小的緩衝區,則後果未定義,因為驅動程式假定數據緩衝區是數據類型的大小,並且不會截截數據以容納較小的緩衝區。 如果應用程式分配了較大的緩衝區,則永遠不會使用額外的空間。  
  
 對於可變長度數據(如字元或二進位數據),請務必認識到數據的位元組長度與緩衝區的位元組長度是分開的,並且通常與緩衝區的位元組長度不同。 這兩個長度的關係在[緩衝區](../../../odbc/reference/develop-app/buffers.md)部分中描述。 如果數據的位元組長度大於緩衝區的位元組長度,驅動程式會截斷提取的數據到緩衝區的位元組長度,並在 SQLSTATE 01004(數據截斷)SQL_SUCCESS_WITH_INFO返回。 但是,返回的位元組長度是未壓縮數據的長度。  
  
 例如,假設應用程式為二進位數據緩衝區分配 50 個字節。 如果驅動程式要返回 10 個字節的二進位資料,它將返回緩衝區中的 10 個字節。 數據的位元組長度為 10,緩衝區的位元組長度為 50。 如果驅動程式要返回 60 個字節的二進位數據,它將數據截截為 50 位元組,返回緩衝區中的這些位元組,並返回SQL_SUCCESS_WITH_INFO。 數據的位元組長度為60(截斷前的長度),緩衝區的位元組長度仍為50。  
  
 為截斷的每個列創建診斷記錄。 由於驅動程式創建這些記錄和應用程式處理這些記錄需要時間,因此截斷可能會降低性能。 通常,應用程式可以通過分配足夠大的緩衝區來避免此問題,儘管在使用長數據時可能無法避免此問題。 當發生數據截斷時,應用程序有時會分配更大的緩衝區並重新提取數據;因此,應用程式可能會重新分配數據。並非在所有情況下都如此。 如果在通過調用**SQLGetData**獲取數據時發生截斷,則應用程式無需為已返回的數據調用**SQLGetData;** 有關詳細資訊,請參閱[獲取長資料](../../../odbc/reference/develop-app/getting-long-data.md)。
