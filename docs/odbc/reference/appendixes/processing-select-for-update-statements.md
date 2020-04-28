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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 904028cd7b3798fcac8f9e5afa6186fae3e9fa29
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81308009"
---
# <a name="processing-select-for-update-statements"></a>處理 SELECT FOR UPDATE 陳述式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 為了達到最大的互通性，應用程式應該會藉由執行**SELECT FOR update**語句來產生結果集，並以定點更新語句進行更新。 雖然資料指標程式庫不需要這麼做，但大部分支援定位 update 語句的資料來源都需要它。  
  
 資料指標程式庫會忽略**SELECT FOR update**語句之**FOR update**子句中的資料行;它會先移除此子句，再將語句傳遞給驅動程式。 在資料指標程式庫中，SQL_ATTR_CONCURRENCY 語句屬性以及上一節所述的限制，會控制是否可以更新結果集中的資料行。
