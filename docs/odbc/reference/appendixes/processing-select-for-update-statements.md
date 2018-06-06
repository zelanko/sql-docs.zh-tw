---
title: 處理 UPDATE 陳述式的選取 |Microsoft 文件
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
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ede999422f6b52112356aa7c9c4b7715eafb96c6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="processing-select-for-update-statements"></a>處理 UPDATE 陳述式的選取
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 最大的互通性，應用程式應該產生一個定位的 update 陳述式會藉由執行更新的結果集**選取更新**陳述式。 雖然資料指標程式庫不需要這個，它需要大部分支援定位的 update 陳述式的資料來源。  
  
 資料指標程式庫會忽略中的資料行**FOR UPDATE**子句**SELECT FOR UPDATE**陳述式; 它會移除這個子句，再將該陳述式傳遞至驅動程式。 在資料指標程式庫，SQL_ATTR_CONCURRENCY 陳述式屬性，以及上一節所述的限制控制項在結果中的資料行設定是否可以更新。
