---
title: 狀態轉換 |微軟文件
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
ms.openlocfilehash: 3a480b7ff8953ef94f0efc4886a09731730a61b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299691"
---
# <a name="state-transitions"></a>狀態轉換
ODBC 為每個環境、每個連線與每個語句定義離散*狀態*。 例如,環境有三種可能狀態:未分配(其中未分配環境)、已分配(其中分配了環境但未分配連接)和連接(其中分配了環境和一個或多個連接)。 連接有七種可能狀態;語句有 13 種可能狀態。  
  
 當應用程式調用某個函數或函數並將句柄傳遞給該項時,由其句柄標識的特定項從一種狀態移動到另一個狀態。 這種運動被稱為*國家過渡*。 例如,使用**SQLAllocHandle**分配環境句柄會將環境從"未分配"移動到"已分配",並且釋放使用**SQLFreeHandle**的句柄將環境從"已分配"返回到"未分配」。 ODBC 定義了數量有限的法律狀態轉換,這是另一種說法,即必須按特定順序調用函數。  
  
 某些函數(如**SQLGetConnectAttr)** 根本不影響狀態。 其他函數會影響單個項的狀態。 例如 **,SQLDisconnect**將連接從連接狀態移動到已分配狀態。 最後,某些函數會影響多個項的狀態。 例如,使用**SQLAllocHandle**分配連接句柄會將連接從未分配移動到已分配狀態,並將環境從「已分配」狀態移動到連接狀態。  
  
 如果應用程式按順序呼叫函數,則函數將傳回*狀態轉換錯誤*。 例如,如果環境處於連接狀態,並且應用程式使用該環境句柄調用**SQLFreeHandle,SQLFreeHandle**將返回 SQLSTATE HY010(函數序列錯誤),因為只有在環境處於已分配狀態時才能**SQLFreeHandle**調用它。 通過將此定義為無效狀態轉換,ODBC 可防止應用程式在有活動連接時釋放環境。  
  
 一些狀態轉換是 ODBC 設計中固有的。 例如,如果不首先分配環境句柄,就無法分配連接句柄,因為分配連接句柄的函數需要環境句柄。 其他狀態轉換由驅動程式管理器和驅動程式強制執行。 例如 **,SQLExecute**執行準備好的語句。 如果傳遞給它的語句句柄未處於準備狀態 **,SQLExecute**將返回 SQLSTATE HY010(函數序列錯誤)。  
  
 從應用程式的角度來看,狀態轉換通常很簡單:法律狀態轉換往往與編寫良好的應用程式流齊頭並進。 狀態轉換對於驅動程式管理器和驅動程序來說更為複雜,因為它們必須跟蹤環境、每個連接和每個語句的狀態。 大部分工作由駕駛員經理完成;驅動程序必須完成的大部分工作都使用具有掛起結果的語句進行。  
  
 本手冊的第 1 部分和第 2 部分("ODBC 簡介"和"開發應用程式和驅動程式")往往沒有明確提及狀態轉換。 相反,它們描述必須調用函數的順序。 例如,"執行語句"指出,必須先使用**SQLPrepare 編寫**語句,然後才能使用**SQLExecute**執行語句。 有關狀態和狀態轉換的完整說明,包括驅動程式管理員檢查哪些轉換,哪些轉換必須由驅動程式檢查,請參閱[附錄 B:ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
