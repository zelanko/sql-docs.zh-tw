---
title: 顯式分配的描述符 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9950bc23a1e75606316039e6c2d66f3dba59940
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305689"
---
# <a name="explicitly-allocated-descriptors"></a>明確配置描述項
應用程式可以在連接到資料庫的任何時候在連接上顯式分配應用程式描述符。 通過將描述符句柄指定為使用**SQLSetStmtAttr**的語句句柄的屬性,應用程式指示驅動程式使用該描述符代替相應的隱式分配的應用程式描述符。 應用程式無法指定備用實現描述符。  
  
 應用程式可以將顯式分配的描述符與多個語句相關聯。 只有當應用程式實際連接到資料庫時,描述符才能是顯式分配的描述符。 應用程式可以顯式釋放此類描述符,也可以通過釋放其連接來隱式釋放。
