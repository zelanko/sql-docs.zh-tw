---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b48951c6fb3be8bfe070863409d77ab760d5fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915610"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>行為變更和 ODBC 3.x 驅動程式
環境屬性 SQL_ATTR_ODBC_VERSION 表示驅動程式是否需要呈現 ODBC *2.x*行為或 ODBC *3.x*行為。 SQL_ATTR_ODBC_VERSION 環境屬性的設定方式，取決於應用程式。 ODBC *3.x*應用程式必須呼叫**SQLSetEnvAttr**來設定這個屬性，在呼叫之後**SQLAllocHandle**配置環境控制代碼，並在呼叫之前**SQLAllocHandle**配置連接控制代碼。 如果電腦無法執行這項操作，驅動程式管理員會傳回 SQLSTATE HY010 （函數順序錯誤） 在第二個呼叫**SQLAllocHandle**。  
  
> [!NOTE]  
>  如需有關行為變更和應用程式如何處理的詳細資訊，請參閱[的行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)。  
  
 ODBC *2.x*應用程式和 ODBC *2.x*重新編譯使用 ODBC 的應用程式*3.x*標頭檔不會呼叫**SQLSetEnvAttr**。 不過，呼叫**SQLAllocEnv**而不是**SQLAllocHandle**配置環境控制代碼。 因此，當應用程式呼叫**SQLAllocEnv**驅動程式管理員 中的驅動程式管理員會呼叫**SQLAllocHandle**並**SQLSetEnvAttr**驅動程式中。 因此，ODBC *3.x*驅動程式一律可以倚賴設定這個屬性。  
  
 如果符合標準的應用程式編譯 ODBC_STD 編譯旗標呼叫**SQLAllocEnv** (這可能是因為**SQLAllocEnv** ISO 中未被取代)，呼叫會對應至**SQLAllocHandleStd**在編譯時期。 在執行階段，應用程式會呼叫**SQLAllocHandleStd**。 驅動程式管理員會設定為 SQL_OV_ODBC3 SQL_ATTR_ODBC_VERSION 環境屬性。 呼叫**SQLAllocHandleStd**相當於呼叫**SQLAllocHandle**具有*HandleType* SQL_HANDLE_ENV 和呼叫**SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 設定為 SQL_OV_ODBC3。  
  
 在特定的驅動程式架構，就會顯示為其中一個 ODBC 驅動程式需要*2.x*驅動程式或 ODBC *3.x*驅動程式，視連線而定。 驅動程式在此情況下可能實際上不是驅動程式，但位於驅動程式管理員和其他驅動程式之間的層。 比方說，它可能會模擬驅動程式，例如 ODBC Spy。 另舉一例，它可能會當作閘道，如 EDA/SQL。 若要顯示為 ODBC *3.x*驅動程式，這樣的驅動程式必須要能夠匯出**SQLAllocHandle**，並顯示為 ODBC *2.x*驅動程式，必須要能夠匯出**SQLAllocConnect**， **SQLAllocEnv**，以及**SQLAllocStmt**。 當環境、 連線或陳述式會配置時，驅動程式管理員將會檢查此驅動程式會匯出**SQLAllocHandle**。 由於驅動程式執行時，此驅動程式管理員會呼叫**SQLAllocHandle**驅動程式中。 如果驅動程式使用 ODBC *2.x*驅動程式，此驅動程式必須將對應的呼叫**SQLAllocHandle**來**SQLAllocConnect**， **SQLAllocEnv**，或**SQLAllocStmt**視需要。 它也必須執行任何動作**SQLSetEnvAttr**行為就像是 ODBC 時，呼叫*2.x*驅動程式。  
  
 此章節包含下列主題。  
  
-   [日期時間資料類型](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [C 資料類型的回溯相容性](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [固定長度書籤](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [SQLGetInfo 支援](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [傳回 SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [呼叫 SQLSetPos 以插入資料](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [依序數載入](../../../odbc/reference/appendixes/loading-by-ordinal.md)
