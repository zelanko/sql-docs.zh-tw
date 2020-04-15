---
title: 隱含式配置的描述符 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 271d479a9d2faa8cd7ab01e02e830b194c4138b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300128"
---
# <a name="implicitly-allocated-descriptors"></a>隱含配置描述項
分配語句句柄時,應用程式隱式分配一組四個描述符。 應用程式可以獲取這些隱式分配的描述符的句柄作為語句句柄的屬性。 當應用程式釋放語句句柄時,驅動程式將釋放該句柄上所有隱式分配的描述符。
