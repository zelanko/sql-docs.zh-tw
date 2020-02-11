---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2512d277980b071523cfea6cbe132f2a3861b7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107293"
---
# <a name="state-transitions"></a>狀態轉換
ODBC 會針對每個環境、每個連接和每個語句定義不同的*狀態*。 例如，環境有三種可能的狀態：未配置（未配置環境）、已配置（已配置環境但未配置任何連線），以及連線（其中的環境和一或多個連接為已配置）。 連接有七個可能的狀態;語句有13個可能的狀態。  
  
 特定專案（由其控制碼識別）會在應用程式呼叫特定函式或函式並將控制碼傳遞給該專案時，從一個狀態移至另一個狀態。 這類移動稱為「*狀態轉換*」。 例如，使用**SQLAllocHandle**配置環境控制碼時，會將環境從未配置的移動到配置，並使用**SQLFreeHandle**釋放該控制碼，並將其從配置的傳回給未配置的。 ODBC 會定義有限數目的合法狀態轉換，這是另一種表示必須以特定順序呼叫函式的方式。  
  
 某些函式（例如**SQLGetConnectAttr**）完全不會影響狀態。 其他函數會影響單一專案的狀態。 例如， **SQLDisconnect**會將連接從線上狀態移動到已配置的狀態。 最後，某些函式會影響一個以上專案的狀態。 例如，使用**SQLAllocHandle**配置連接控制碼時，會將未配置的連接移到已配置的狀態，並將環境從配置的移到連接狀態。  
  
 如果應用程式依序呼叫函式，函數會傳回*狀態轉換錯誤*。 例如，如果環境處於線上狀態，而應用程式使用該環境控制碼呼叫**SQLFreeHandle** ，則**SQLFREEHANDLE**會傳回 SQLSTATE HY010 （函式序列錯誤），因為只有在環境處於已配置的狀態時，才會呼叫它。 藉由將此定義為不正確狀態轉換，ODBC 可防止應用程式在有作用中的連接時釋放環境。  
  
 某些狀態轉換在 ODBC 的設計上是固有的。 例如，您不能在沒有第一次配置環境控制碼的情況下配置連接控制碼，因為配置連接控制碼的函式需要環境控制碼。 驅動程式管理員和驅動程式會強制執行其他狀態轉換。 例如， **SQLExecute**會執行備妥的語句。 如果傳遞給它的語句控制碼不是處於備妥狀態， **SQLExecute**會傳回 SQLSTATE HY010 （函數序列錯誤）。  
  
 從應用程式的觀點來看，狀態轉換通常是直接的：法律狀態轉換傾向于與撰寫完善的應用程式流程。 驅動程式管理員和驅動程式的狀態轉換更為複雜，因為它們必須追蹤環境的狀態、每個連接，以及每個語句。 這大部分的工作都是由驅動程式管理員來完成;大部分必須由驅動程式完成的工作，都是以具有暫止結果的語句來進行。  
  
 本手冊的第1部分和第2部分（「ODBC 簡介」和「開發應用程式和驅動程式」）傾向于不明確提及狀態轉換。 相反地，它們會描述函數必須呼叫的順序。 例如，「執行語句」表示語句必須使用**SQLPrepare**來準備，才能使用**SQLExecute**來執行。 如需狀態和狀態轉換的完整描述，包括驅動程式管理員所檢查的轉換，以及驅動程式必須檢查哪些轉換，請參閱[附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
