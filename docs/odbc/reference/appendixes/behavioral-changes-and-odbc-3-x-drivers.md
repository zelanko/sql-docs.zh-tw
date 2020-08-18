---
description: 行為變更和 ODBC 3.x 驅動程式
title: 行為變更和 ODBC 3.x 驅動程式 |Microsoft Docs
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
ms.openlocfilehash: 43f64aa4b627130308ea920918c2de6d98116020
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411334"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>行為變更和 ODBC 3.x 驅動程式
環境屬性 SQL_ATTR_ODBC_VERSION 指出驅動程式是否需要展示 ODBC 2.x*行為或*odbc *3.x 行為。* 如何設定 SQL_ATTR_ODBC_VERSION 環境屬性取決於應用程式。 ODBC *3.x*應用程式必須在呼叫**SQLAllocHandle**來配置環境控制碼之後，以及呼叫**SQLAllocHandle**來配置連接控制碼之前，呼叫**SQLSetEnvAttr**來設定這個屬性。 如果無法這麼做，驅動程式管理員會在對 **SQLAllocHandle**的第二個呼叫上，傳回 SQLSTATE HY010 (函數順序) 錯誤。  
  
> [!NOTE]  
>  如需行為變更和應用程式運作方式的詳細資訊，請參閱 [行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 以 ODBC *3.x 標頭檔*重新編譯*的 odbc 2.x 應用程式和*odbc *2.x 應用程式*不會呼叫**SQLSetEnvAttr**。 不過，它們會呼叫 **SQLAllocEnv** 而不是 **SQLAllocHandle** 來配置環境控制碼。 因此，當應用程式在驅動程式管理員中呼叫 **SQLAllocEnv** 時，驅動程式管理員會在驅動程式中呼叫 **SQLAllocHandle** 和 **SQLSetEnvAttr** 。 因此 *，ODBC 3.x* 驅動程式一律會在設定此屬性時計算。  
  
 如果以 ODBC_STD 編譯旗標編譯符合標準的應用程式呼叫 **SQLAllocEnv** (可能是因為 **SQLALLOCENV** 未在 ISO) 中淘汰，則呼叫會在編譯時期對應到 **SQLAllocHandleStd** 。 在執行時間，應用程式會呼叫 **SQLAllocHandleStd**。 驅動程式管理員會將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3。 對**SQLAllocHandleStd**的呼叫相當於呼叫*HandleType*為 SQL_HANDLE_ENV 的**SQLAllocHandle** ，以及對**SQLSetEnvAttr**的呼叫，以將 SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC3。  
  
 在某些驅動程式架構中，視連接而定，驅動程式必須顯示為 ODBC 2.x 驅動程式*或 odbc* *3.x 驅動程式*。 在此情況下，驅動程式可能不是驅動程式，而是位於驅動程式管理員與另一個驅動程式之間的一層。 例如，它可能會模仿像 ODBC Spy 的驅動程式。 在另一個範例中，它可能會做為閘道，例如 EDA/SQL。 若要顯示為 ODBC 3.x 驅動程式，這類驅動程式必須能夠匯出**SQLAllocHandle**，並且顯示*為 odbc 2.x* *驅動程式，* 必須能夠匯出**SQLAllocConnect**、 **SQLAllocEnv**和**SQLAllocStmt**。 配置環境、連線或語句時，驅動程式管理員會檢查此驅動程式是否匯出 **SQLAllocHandle**。 驅動程式會在驅動程式中呼叫 SQLAllocHandle，因此驅動程式管理員會在驅動程式中呼叫**SQLAllocHandle** 。 如果 *驅動程式正在使用 ODBC 2.x* 驅動程式，則驅動程式必須適當地將 **SQLAllocHandle** 的呼叫對應至 **SQLAllocConnect**、 **SQLAllocEnv**或 **SQLAllocStmt**。 在做*為 ODBC 2.x*驅動程式時，也必須使用**SQLSetEnvAttr**呼叫來執行任何動作。  
  
 此章節包含下列主題。  
  
-   [日期時間資料類型](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 資料類型的回溯相容性](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [固定長度書籤](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 支援](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [傳回 SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [呼叫 SQLSetPos 以插入資料](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [依序數載入](../../../odbc/reference/appendixes/loading-by-ordinal.md)
