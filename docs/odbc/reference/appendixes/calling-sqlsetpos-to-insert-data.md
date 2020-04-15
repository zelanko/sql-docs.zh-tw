---
title: 呼叫 SQLSetPos 以插入資料 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb374b2506d55b400207c8f60bdf42bb6bb4065e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306599"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>呼叫 SQLSetPos 以插入資料
使用 ODBC *3. x*驅動程式的 ODBC *2.x*應用程式呼叫**SQLSetPos**時,*操作*參數為 SQL_ADD,驅動程式管理器不會將此呼叫映射到**SQLBulk 操作**。 如果 ODBC *3.x*驅動程式應使用使用 SQL_ADD 調用**SQLSetPos**的應用程式,則驅動程式應支援該操作。  
  
 當使用 SQL_ADD調用**SQLSetPos**時,行為上會出現一個主要差異,當在狀態 S6 中調用 SQLSetPos 時。 在 ODBC *2.x*中,當 SQLSetPos 在狀態 S6 中呼叫 SQL_ADD **sqlSetPos**時(在游標已使用**SQLFetch**定位後),驅動程式傳回 S1010。 在 ODBC *3.x*中,可在狀態 S6 中呼叫操作*SQL_ADD的***SQLBulk 操作**。 行為的第二個主要區別是,具有SQL_ADD*操作*的**SQLBulk 操作**可以在狀態 S5 中調用,而操作**SQL_ADD的****SQLSetPos**不能調用。 有關 ODBC *3.x*中同一呼叫可能發生的語句轉換,請參閱[附錄 B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
