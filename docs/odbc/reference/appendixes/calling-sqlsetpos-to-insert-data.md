---
description: 呼叫 SQLSetPos 以插入資料
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 215d02e9b5bd92f6a22f7e45c8c29c7c5a0a6a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449010"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>呼叫 SQLSetPos 以插入資料
當*使用 odbc 3.x* *驅動程式的 odbc* 2.x 應用程式呼叫*SQL_ADD 的作業引數* **SQLSetPos**時，驅動程式管理員不會將此呼叫對應至**SQLBulkOperations**。 如果 *ODBC 3.x 驅動程式應* 與使用 SQL_ADD 呼叫 **SQLSetPos** 的應用程式搭配使用，則驅動程式應該支援該操作。  
  
 使用 SQL_ADD 呼叫 **SQLSetPos** 時，會發生一個主要的差異，在狀態 S6 中呼叫時會發生此情況。 在 ODBC *2.x*中，此驅動程式會在資料指標已定位於**SQLFetch**) 之後 (使用 SQL_ADD 在狀態 S6 中呼叫**SQLSetPos**時傳回 S1010。 在 ODBC *3.x 中，* SQLBulkOperations 作業*SQL_ADD 的* **SQLBulkOperations**可在狀態 S6 中呼叫。 行為的第二個主要差異是， **SQLBulkOperations** *操作* SQL_ADD 可在狀態 S5 中呼叫，而 **SQLSetPos** 則無法 SQL_ADD **運作** 。 如需 ODBC 3.x 中相同呼叫所能發生的語句轉換 *，請參閱*[附錄 B： Odbc 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
