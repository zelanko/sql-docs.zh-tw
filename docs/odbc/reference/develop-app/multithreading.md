---
title: 多執行緒處理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1eaa07ce22436bc8bfae215c0431480081ee0f06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086355"
---
# <a name="multithreading"></a>多執行緒
多執行緒在作業系統上，驅動程式必須是安全執行緒。 也就是它必須是應用程式可能要在多個執行緒上使用相同的控制代碼。 如何達成這是驅動程式特有，而且很可能驅動程式將會序列化任何嘗試同時在兩個不同的執行緒上使用相同的控制代碼。  
  
 應用程式通常使用多個執行緒，而不是非同步處理。 應用程式建立個別的執行緒呼叫 ODBC 函數，然後在主執行緒上繼續處理。 而不必持續輪詢的非同步函式，在此情況下使用 sql_attr_async_enable 設定陳述式屬性時，應用程式可以直接讓新建立的執行緒完成。  
  
 可接受的陳述式控制代碼，以及一個執行緒上執行的函式可以藉由呼叫取消**SQLCancel**使用相同的陳述式，從另一個執行緒處理。 雖然驅動程式不應該序列化的用法**SQLCancel**這種方式，則無法保證，呼叫**SQLCancel**實際上將會取消另一個執行緒上執行的函式。
