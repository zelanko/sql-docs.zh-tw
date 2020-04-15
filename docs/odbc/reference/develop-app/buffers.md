---
title: 緩衝區 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c49e83e12463665f86f8cc15dc595e6ba2c506f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306283"
---
# <a name="buffers"></a>緩衝區
緩衝區是用於在應用程式和驅動程序之間傳遞數據的任何應用程式記憶體。 例如,應用程式緩衝區可以與**SQLBindCol**關聯或*綁定到*結果集列。 獲取每行時,將返回這些緩衝區中每一列的數據。 *輸入緩衝區*用於將數據從應用程式傳遞到驅動程式;*輸出緩衝區*用於將數據從驅動程式返回到應用程式。  
  
> [!NOTE]  
>  如果 ODBC 函數傳回SQL_ERROR,則該函數的任何輸出參數的內容都是未定義的。  
  
 此討論主要涉及不確定類型的緩衝區。 這些緩衝區的位址顯示為 SQLPOINTER 類型的參數,如**SQLBindCol**中的*TargetValuePtr*參數。 但是,此處討論的某些項(如用於緩衝區的參數)也適用於用於將字串傳遞給驅動程式的參數,如**SQLTable**中的*表名稱*參數。  
  
 這些緩衝區通常成對。 *數據緩衝區*用於傳遞數據本身,而*長度/指示器緩衝區*用於傳遞數據緩衝區中的數據長度或特殊值(如SQL_NULL_DATA),指示數據為 NULL。 數據緩衝區中的數據長度與數據緩衝區本身的長度不同。 下圖顯示了數據緩衝區與長度/指示器緩衝區之間的關係。  
  
 ![資料緩衝區和長度&#47;指示器緩衝區](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 每當數據緩衝區包含可變長度數據(如字元或二進位資料)時,都需要長度/指示器緩衝區。 如果數據緩衝區包含固定長度數據(如整數或日期結構),則僅需要長度/指示器緩衝區來傳遞指標值,因為數據的長度已為人所知。 如果應用程式使用長度/指示器緩衝區與固定長度數據,驅動程式將忽略其中傳遞的任何長度。  
  
 數據緩衝區及其包含的數據的長度以位元組為單位進行測量,而不是以字元為單位。 這種區別對於使用 ANSI 字串的程序來說並不重要,因為位元組和字元的長度是相同的。  
  
 當數據緩衝區表示驅動程式定義的描述符欄位、診斷欄位或屬性時,應用程式應向驅動程式管理員指示指示欄位或屬性值的函數參數的性質。 應用程式通過在將欄位或屬性設置為以下值之一的任何函數調用中設置 length 參數來進行此種操作。 (檢索欄位或屬性值的函數也是如此,但參數指向設置函數本身的值除外。  
  
-   如果指示欄位或屬性值的函數參數是指向字串的指標,則*長度*參數是字串的長度或SQL_NTS。  
  
-   如果指示欄位或屬性值的函數參數是指向二進位緩衝區的指標,則應用程式將在*長度*參數中放置SQL_LEN_BINARY_ATTR(*長度*)宏的結果。 這將在*長度*參數中放置負值。  
  
-   如果指示欄位或屬性值的函數參數是指向字串或二進位字串以外的值的指標,*則長度*參數應具有值SQL_IS_POINTER。  
  
-   如果指示欄位或屬性值的函數參數包含固定長度值,則*長度*參數將根據需要SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或SQL_ISI_USMALLINT。  
  
 此章節包含下列主題。  
  
-   [延遲的緩衝區](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [配置及釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [使用資料緩衝區](../../../odbc/reference/develop-app/using-data-buffers.md)
