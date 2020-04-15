---
title: 行為變化和 ODBC 3.x 驅動程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8343573261d74a6a0c652cf425b12da91f7cb0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292362"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>行為變更和 ODBC 3.x 驅動程式
環境屬性SQL_ATTR_ODBC_VERSION向驅動程式指示是否需要顯示 ODBC *2.x*行為還是 ODBC *3.x*行為。 SQL_ATTR_ODBC_VERSION環境屬性的設置方式取決於應用程式。 ODBC *3.x*應用程式在調用**SQLAllocHandle**以分配環境句柄之前,在調用**SQLAllocHandle**以分配連接句柄之前,必須調用**SQLSetEnvAttr**來設置此屬性。 如果他們未能執行此操作,驅動程式管理器將在後者調用**SQLAllocHandle**時返回 SQLSTATE HY010(函數序列錯誤)。  
  
> [!NOTE]  
>  有關行為更改和應用程式行為方式的詳細資訊,請參閱[行為更改](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 ODBC *2.x*應用程式和 ODBC *2.x*應用程式使用 ODBC *3.x*標頭檔重新編譯,不呼叫**SQLSetEnvAttr**。 但是,他們調用**SQLAllocEnv**而不是**SQLAllocHandle**來分配環境句柄。 因此,當應用程式在驅動程式管理器中調用**SQLAllocEnv**時,驅動程式管理器在驅動程式中調用**SQLAllocHandle**和**SQLSetEnvAttr。** 因此,ODBC *3.x*驅動程式始終可以依賴於正在設置此屬性。  
  
 如果使用ODBC_STD編譯標誌編譯的符合標準的應用程式調用**SQLAllocEnv(** 這可能是由於**SQLAllocEnv**在 ISO 中未棄用而發生的),則調用在編譯時映射到**SQLAlloc HandleStd。** 在執行時,應用程式呼叫**SQLAllocHandleStd**。 驅動程式管理員將SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC3。 對**SQLAllocHandleStd**的調用等效於對**SQLAllocHandle**的調用,該調用具有SQL_HANDLE_ENV*的句柄類型*,以及對**SQLSetEnv Attr**的調用,以將SQL_ATTR_ODBC_VERSION設置為SQL_OV_ODBC3。  
  
 在某些驅動程式體系結構中,驅動程式需要顯示為 ODBC *2.x*驅動程式或 ODBC *3.x*驅動程式,具體取決於連接。 在這種情況下,驅動程式實際上可能不是驅動程式,而是位於驅動程式管理器和另一個驅動程式之間的層。 例如,它可能模仿驅動程式,如 ODBC 間諜。 在另一個示例中,它可能充當閘道,如 EDA/SQL。 要顯示為 ODBC *3.x*驅動程式,此類驅動程式必須能夠匯出**SQLAllocHandle,** 並且要顯示為 ODBC *2.x*驅動程式,必須能夠匯出**SQLAllocConnect、SQLAllocEnv**和**SQLAllocStmt**。 **SQLAllocEnv** 配置環境、連線或語句時,驅動程式管理員將檢查此驅動程式是否匯出**SQLAllocHandle**。 由於驅動程式確實如此,驅動程式管理器在驅動程式中調用**SQLAllocHandle。** 如果驅動程式使用 ODBC *2.x*驅動程式,則驅動程式必須根據需要將呼叫映射到**SQLAllocHandle、SQLAllocEnv**或**SQLAllocStmt。** **SQLAllocHandle** **SQLAllocEnv** 當作為 ODBC *2.x*驅動程式執行時,它還必須對**SQLSetEnvAttr**調用執行任何操作。  
  
 此章節包含下列主題。  
  
-   [日期時間資料類型](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 資料類型的回溯相容性](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [固定長度書籤](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 支援](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [傳回 SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [呼叫 SQLSetPos 以插入資料](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [依序數載入](../../../odbc/reference/appendixes/loading-by-ordinal.md)
