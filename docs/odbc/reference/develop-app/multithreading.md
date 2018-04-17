---
title: 多執行緒 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e2ad7121936734e30795de2153c06c14595f638
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="multithreading"></a>多執行緒處理
多執行緒在作業系統上，驅動程式必須具備執行緒安全。 也就是說，必須是可將多個執行緒上使用相同的控制代碼的應用程式。 這達成特定驅動程式和它可能會驅動程式會序列化任何嘗試同時在兩個不同的執行緒上使用相同的控制代碼。  
  
 應用程式通常使用多個執行緒，而不是非同步處理。 應用程式建立個別的執行緒、 呼叫 ODBC 函數，並再繼續處理，在主執行緒上。 而不必持續輪詢非同步函式，在此情況下使用 SQL_ATTR_ASYNC_ENABLE 陳述式屬性時，應用程式可以直接讓新建立的執行緒完成。  
  
 接受陳述式控制代碼，以及一個執行緒上執行的函式可以藉由呼叫取消**SQLCancel**相同陳述式，從另一個執行緒處理。 雖然驅動程式不應該序列化使用**SQLCancel**這種方式，並不保證呼叫**SQLCancel**實際上將會取消另一個執行緒上執行的函式。
