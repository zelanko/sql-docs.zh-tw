---
description: 處理 SELECT FOR UPDATE 陳述式
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
ms.openlocfilehash: 74d32298ca9303c0c82a0810e558cace6b957b8b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483183"
---
# <a name="processing-select-for-update-statements"></a>處理 SELECT FOR UPDATE 陳述式
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 為了達到最大的互通性，應用程式應該會產生結果集，並藉由執行 **SELECT FOR update** 語句，以定位的 update 語句進行更新。 雖然資料指標程式庫不需要這項功能，但支援定點更新語句的大部分資料來源都需要它。  
  
 資料指標程式庫會忽略**SELECT FOR update**語句的**FOR update**子句中的資料行;它會先移除這個子句，然後再將語句傳遞至驅動程式。 在資料指標程式庫中，SQL_ATTR_CONCURRENCY 語句屬性以及上一節中所述的限制，會控制是否可以更新結果集內的資料行。
