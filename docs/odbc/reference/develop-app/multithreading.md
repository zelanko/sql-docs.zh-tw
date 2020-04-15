---
title: 多線程 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10d1b401ac780d24184c4c2337199e99973e916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302410"
---
# <a name="multithreading"></a>多執行緒
在多線程操作系統上,驅動程式必須具有線程安全。 也就是說,應用程式必須可以在多個線程上使用相同的句柄。 如何實現這一點特定於驅動程式,並且驅動程式可能會序列化在兩個不同的線程上同時使用相同的句柄的任何嘗試。  
  
 應用程式通常使用多個線程而不是非同步處理。 應用程式創建一個單獨的線程,調用它上的 ODBC 函數,然後在主線程上繼續處理。 與使用SQL_ATTR_ASYNC_ENABLE語句屬性時那樣,不必持續輪詢異步函數,應用程式只需讓新創建的線程完成即可。  
  
 可以接受語句句柄並在一個線程上運行的函數可以通過調用**SQLCancel**與另一個線程中的相同語句句柄來取消。 儘管驅動程式不應以這種方式序列化**SQLCancel**的使用,但不能保證調用**SQLCancel**實際上會取消在其他線程上運行的函數。
