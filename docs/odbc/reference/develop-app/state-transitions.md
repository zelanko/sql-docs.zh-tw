---
title: 狀態轉換 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 424c421b29dce6bedad9a73c1d27acb01b6e77c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="state-transitions"></a>狀態轉換
ODBC 定義離散*狀態*每個環境中，每個連接，和每個陳述式。 例如，環境有三種可能狀態： 未配置的 （在其任何環境配置），已配置 （所在環境配置，但沒有連線配置），並連接 （所在的環境和一個或多個連接都是已配置）。 連接具有七個可能的狀態。陳述式有 13 的可能狀態。  
  
 特定的項目，當由其控制代碼，移到從某個狀態到另一個應用程式呼叫某個函式或函式，並將控制代碼傳遞給該項目時。 這類移動稱為*狀態轉換*。 例如，配置環境控制代碼與**SQLAllocHandle**將環境從未配置移到已配置，並釋放該控制代碼與**SQLFreeHandle**傳回從已配置到未配置。 ODBC 定義有限的數目的合法的狀態轉換，這是另一種方式的說法，必須以特定順序呼叫函式。  
  
 某些函式，例如**SQLGetConnectAttr**，完全不影響狀態。 其他函式會影響單一項目的狀態。 例如， **SQLDisconnect**將連接從連接狀態移至已配置的狀態。 最後，某些函式會影響多個項目的狀態。 例如，配置連接控制代碼與**SQLAllocHandle**從未配置的連接將已配置狀態，並將環境從已配置移到連接的狀態。  
  
 如果應用程式呼叫的函式不按順序，則此函數會傳回*狀態轉換錯誤*。 例如，如果環境處於連線狀態和應用程式呼叫**SQLFreeHandle**與該環境控制代碼， **SQLFreeHandle**傳回 SQLSTATE HY010 （函數順序錯誤）因為只有在環境處於 已配置的狀態時，才可以呼叫它。 藉由定義這與無效的狀態轉換，ODBC 會防止應用程式有使用中連接時釋放環境。  
  
 在設計中的 ODBC 一定會有某些狀態轉換。 例如，不可能因為配置連接控制代碼的函式需要環境控制代碼，而不需第一個配置環境控制代碼配置連接控制代碼。 其他的狀態轉換會強制執行驅動程式管理員及驅動程式。 例如， **SQLExecute**執行備妥的陳述式。 如果陳述式控制代碼傳遞給它不在已備妥狀態， **SQLExecute**傳回 SQLSTATE HY010 （函數順序錯誤）。  
  
 從應用程式的觀點來看，狀態轉換會使用通常直接： 合法的狀態轉換傾向於移手中手動編寫完善的應用程式的流程。 狀態轉換是更複雜的驅動程式管理員及驅動程式，因為它們必須追蹤狀態的環境、 每個連接及每個陳述式。 大部分的這項工作是由驅動程式管理員。陳述式具有擱置的結果也會發生的大部分工作，必須由驅動程式。  
  
 本手冊的部分 1 和 2 (< ODBC 簡介"和"開發應用程式和驅動程式 」) 較不明確指定狀態轉換。 相反地，它們會描述函式必須呼叫的順序。 例如，「 執行陳述式 」 狀態陳述式，必須備妥與**SQLPrepare**可以使用執行前**SQLExecute**。 如需完整的狀態和狀態轉換，包括轉換會檢查驅動程式管理員，且其必須檢查驅動程式，說明請參閱[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
