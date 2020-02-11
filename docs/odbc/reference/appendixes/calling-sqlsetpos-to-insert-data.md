---
title: 呼叫 SQLSetPos 以插入資料 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e07bf71f0d622ad9095974cd7020001625edf1f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037713"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>呼叫 SQLSetPos 以插入資料
當 ODBC 2.x*應用程式**與 odbc 3.x*驅動程式搭配使用 SQL_ADD 的*Operation*引數呼叫**SQLSetPos**時，驅動程式管理員不會將此呼叫對應至**SQLBulkOperations**。 如果*ODBC 3.x 驅動程式應該*與使用 SQL_ADD 呼叫**SQLSetPos**的應用程式搭配運作，驅動程式應該會支援該作業。  
  
 以 SQL_ADD 呼叫**SQLSetPos**時，會發生一個主要的差異，在狀態 S6 中呼叫它時。 在 ODBC *2.x 中，* 當以狀態 S6 中的 SQL_ADD 呼叫**SQLSetPos**時，驅動程式會傳回 S1010 （在將游標置於**SQLFetch**之後）。 在 ODBC *3.x 中，* 可以在狀態 S6 中呼叫具有 SQL_ADD*作業的* **SQLBulkOperations** 。 行為*的第*二個主要差異在於**SQLBulkOperations**具有 SQL_ADD 的作業可以在狀態 S5 中呼叫，而 SQL_ADD **SQLSetPos** **的作業則**不能。 如*需 odbc 3.x 中相同*呼叫可能發生的語句轉換，請參閱[附錄 B： Odbc 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
