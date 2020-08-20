---
description: 狀態轉換
title: 狀態轉換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 947be49fc0a77f94c1641bb7c735db3276b49f58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476360"
---
# <a name="state-transitions"></a>狀態轉換
ODBC 為每個環境、每個連接和每個語句定義了離散的 *狀態* 。 例如，環境有三個可能的狀態：未配置的 (不會配置任何環境) 、配置 (（配置環境），但不會配置) 的連接，以及 (配置一個或多個連線的連接) 。 連接具有七個可能的狀態;語句有13個可能的狀態。  
  
 當應用程式呼叫特定的函式或函式，並將控制碼傳遞給該專案時，以其控制碼識別的特定專案會從某個狀態移至另一個狀態。 這類移動稱為「 *狀態」轉換*。 例如，使用 **SQLAllocHandle** 配置環境控制碼，會將環境從未配置的配置移至已配置，並使用 **SQLFreeHandle** 釋放該控制碼，將其從配置到未配置的。 ODBC 定義了有限數量的合法狀態轉換，這是另一種表示函式必須以特定順序來呼叫的方式。  
  
 某些函式（例如 **SQLGetConnectAttr**）完全不會影響狀態。 其他函式會影響單一專案的狀態。 例如， **SQLDisconnect** 會將連接從連接狀態移動到已配置的狀態。 最後，某些函數會影響多個專案的狀態。 例如，使用 **SQLAllocHandle** 配置連接控制碼，會將連接從未配置的連線移至已配置的狀態，並將環境從配置的連接狀態移到連接狀態。  
  
 如果應用程式依序呼叫函式，則函式會傳回 *狀態轉換錯誤*。 例如，如果環境處於連接狀態，而應用程式使用該環境控制碼呼叫 **SQLFreeHandle** ，則 **SQLFREEHANDLE** 會傳回 SQLSTATE HY010 (函式順序錯誤) ，因為它只能在環境處於已配置狀態時呼叫。 藉由將此定義為不正確狀態轉換，ODBC 會防止應用程式在有使用中的連接時釋放環境。  
  
 某些狀態轉換在 ODBC 設計中是固有的。 例如，因為配置連接控制碼的函式需要環境控制碼，所以無法在未先配置環境控制碼的情況下配置連接控制碼。 驅動程式管理員和驅動程式會強制執行其他狀態轉換。 例如， **SQLExecute** 會執行備妥的語句。 如果傳遞給它的語句控制碼未處於備妥狀態， **SQLExecute** 會傳回 SQLSTATE HY010 (函數順序錯誤) 。  
  
 從應用程式的觀點來看，狀態轉換通常很簡單：法律狀態轉換通常會與妥善撰寫之應用程式的流程並存。 驅動程式管理員和驅動程式的狀態轉換較為複雜，因為它們必須追蹤環境的狀態、每個連接，以及每個語句。 這項工作大多是由驅動程式管理員所完成;大部分必須由驅動程式完成的工作會與具有暫止結果的語句一起發生。  
  
 本手冊的第1和第2部分 ( 「ODBC 簡介」和「開發應用程式和驅動程式」 ) 傾向于不明確提及狀態轉換。 相反地，它們會描述函數必須呼叫的順序。 例如，「執行語句」指出必須使用 **SQLPrepare** 來準備語句，才能以 **SQLExecute**執行。 如需狀態和狀態轉換的完整說明，包括驅動程式管理員所檢查的轉換，以及哪些驅動程式必須由驅動程式檢查，請參閱 [附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
