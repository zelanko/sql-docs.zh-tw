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
manager: craigg
ms.openlocfilehash: 30c1db4f850e6f181757d974ae74bb475b0cc5cc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63148995"
---
# <a name="state-transitions"></a>狀態轉換
ODBC 定義離散*狀態*每個環境中，每個連線，和每個陳述式。 例如，環境會有三種可能狀態：未配置 （在而無環境在配置），已配置 （所在環境配置，但沒有連線會配置） 和 （所在的環境和一個或多個連線都已配置） 的連線。 連接有七個可能的狀態;陳述式有 13 的可能狀態。  
  
 特定的項目，均由其控制代碼，從某個狀態移轉到另一個應用程式呼叫某個函式或函式，並將控制代碼傳遞給該項目時。 呼叫這類移動*狀態轉換*。 比方說，配置環境控制代碼**SQLAllocHandle**為由未配置中的環境，已配置，並釋放與該控制代碼**SQLFreeHandle**傳回從已配置到未配置。 ODBC 定義有限的數量的合法的狀態轉換，這是另一種表示，必須以特定順序呼叫函式。  
  
 某些函式，例如**SQLGetConnectAttr**，完全不影響狀態。 其他函式會影響單一項目的狀態。 例如， **SQLDisconnect**將連接從連接狀態移至 已配置狀態。 最後，有些函式會影響多個項目的狀態。 例如，配置連接控制代碼與**SQLAllocHandle**移動的未配置的連線已配置狀態，並將環境從 Allocated 移到連接的狀態。  
  
 如果應用程式會呼叫不按順序的函式，則此函數會傳回*狀態轉換錯誤*。 例如，如果環境是在連線狀態和應用程式中呼叫**SQLFreeHandle**與該環境控制代碼， **SQLFreeHandle**傳回 SQLSTATE HY010 （函數順序錯誤）因為只有在環境處於已配置的狀態時，才可以呼叫它。 藉由定義這為狀態轉換無效，ODBC 會防止應用程式有使用中連接時釋放環境。  
  
 在設計中的 ODBC 一定會有一些狀態轉換。 比方說，不可能因為配置連接控制代碼的函式需要環境控制代碼，而不需第一個配置環境控制代碼，配置連接控制代碼。 其他的狀態轉換會強制執行驅動程式管理員及驅動程式。 例如， **SQLExecute**執行備妥的陳述式。 如果陳述式控制代碼傳遞給它不在已準備就緒的狀態， **SQLExecute**傳回 SQLSTATE HY010 （函數順序錯誤）。  
  
 從應用程式的觀點來看，狀態轉換為通常直接了當：合法的狀態轉換通常會前往手中手動撰寫得當的應用程式的流程。 狀態轉換是更複雜的驅動程式管理員和驅動程式，因為它們必須追蹤環境中，每個連線，以及每個陳述式的狀態。 大部分的這項工作是由驅動程式管理員;大部分的工作，必須由驅動程式發生在陳述式與暫止的結果。  
  
 本手冊的部分 1 和 2 (「 ODBC 簡介 」 和 「 開發應用程式和驅動程式 」) 不容易明確提及狀態轉換。 相反地，它們會說明必須呼叫函式的順序。 比方說，「 執行陳述式 」 狀態，必須使用準備陳述式**SQLPrepare**可以使用執行前**SQLExecute**。 如需完整描述的狀態和狀態轉換，包括轉換會檢查驅動程式管理員，且其必須進行檢查驅動程式，請參閱[附錄 b:狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
