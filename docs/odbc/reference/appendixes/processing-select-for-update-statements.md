---
title: 處理 SELECT FOR UPDATE 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ad9a20ab8abd40123ec4e4d7369373e68699205
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028373"
---
# <a name="processing-select-for-update-statements"></a>處理 SELECT FOR UPDATE 陳述式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 為了達到最大的互通性，應用程式應該會藉由執行**SELECT FOR update**語句來產生結果集，並以定點更新語句進行更新。 雖然資料指標程式庫不需要這麼做，但大部分支援定位 update 語句的資料來源都需要它。  
  
 資料指標程式庫會忽略**SELECT FOR update**語句之**FOR update**子句中的資料行;它會先移除此子句，再將語句傳遞給驅動程式。 在資料指標程式庫中，SQL_ATTR_CONCURRENCY 語句屬性以及上一節所述的限制，會控制是否可以更新結果集中的資料行。
