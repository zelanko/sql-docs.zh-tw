---
title: 驅動程式管理器&#39;連接過程中的角色 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0227a4063573cb05ecaa9434605ba35f2811bd06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305799"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>驅動程式管理員&#39;連接過程中的角色
請記住,應用程式不直接調用驅動程式函數。 相反,它們調用具有相同名稱的驅動程式管理員函數,驅動程式管理器呼叫驅動程式函數。 通常,這種情況幾乎立即發生。 例如,應用程式在驅動程式管理器中調用**SQLExecute,** 在進行幾次錯誤檢查後,驅動程式管理器在驅動程式中調用**SQLExecute。**  
  
 連接過程不同。 當應用程式使用SQL_HANDLE_ENV和SQL_HANDLE_DBC選項調用**SQLAllocHandle**時,該函數僅在驅動程式管理器中分配句柄。 驅動程式管理員不會在驅動程式中調用此函數,因為它不知道要調用哪個驅動程式。 同樣,如果應用程式將未連接的連接的句柄傳遞給**SQLSetConnectAttr**或**SQLGetConnectAttr,** 則只有驅動程式管理器執行該函數。 它存儲或獲取其連接句柄的屬性值,並在獲取尚未設置且 ODBC 未為其定義預設值的屬性的值時返回 SQLSTATE 08003(連接未打開)。  
  
 當應用程式呼叫**SQLConnect** **、SQLDriverConnect**或**SQLBrowseConnect**時,驅動程式管理員首先確定要使用的驅動程式。 然後,它會檢查以確定當前是否在連接上載入了驅動程式:  
  
-   如果連接上未載入驅動程式,則驅動程式管理員將檢查指定驅動程式是否在同一環境中的另一個連接上載入。 如果沒有,驅動程式管理器將驅動程式載入到連接上,並在驅動程式中使用SQL_HANDLE_ENV選項調用**SQLAllocHandle。**  
  
     然後,驅動程式管理器在驅動程式中使用SQL_HANDLE_DBC選項調用**SQLAllocHandle,** 無論是否剛剛載入。 如果應用程式設定了任何連接屬性,驅動程式管理器在驅動程式中調用**SQLSetConnectAttr;如果驅動程式中調用 SQLSetConnectAttr;如果驅動程式中調用 SQLSetConnectAttr,則驅動程式將調用 SQLSetConnectAttr。** 如果發生錯誤,驅動程式管理員的連接函數將返回 SQLSTATE IM006(驅動程式的**SQLSetConnectAttr**失敗)。 最後,驅動程式管理器調用驅動程式中的連接函數。  
  
-   如果在連接上載入了指定的驅動程式,則驅動程式管理器僅調用驅動程式中的連接功能。 在這種情況下,驅動程式必須確保連接上的所有連接屬性都保持其當前設置。  
  
-   如果連接上載入了其他驅動程式,驅動程式管理器會調用驅動程式中的**SQLFreeHandle**以釋放連接。 如果沒有使用驅動程式的其他連接,驅動程式管理器在驅動程式中調用**SQLFreeHandle**以釋放環境並卸載驅動程式。 然後,驅動程式管理器執行與未在連接上載入驅動程式時相同的操作。  
  
 當*HandleType*設定為**SQL_HANDLE_DBC**時,驅動程式管理器將鎖定環境句柄 *(henv),* 然後再調用驅動程式的**SQLAllocHandle**和**SQLFreeHandle。**  
  
 當應用程式呼叫**SQLDISCONNECT**時,驅動程式管理器在驅動程式中調用**SQLDISCONNECT。** 但是,它會在應用程式重新連接到驅動程序的情況下載入驅動程式。 當應用程式使用SQL_HANDLE_DBC選項調用**SQLFreeHandle**時,驅動程式管理器在驅動程序中調用**SQLFreeHandle。** 如果驅動程式未被任何其他連接使用,則驅動程式管理器然後在驅動程式中調用**SQLFreeHandle,** 並帶有SQL_HANDLE_ENV選項並卸載驅動程式。
