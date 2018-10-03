---
title: 處理 SELECT FOR UPDATE 陳述式 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7f54d31426773f294a4a23f059c9f906d430056f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721756"
---
# <a name="processing-select-for-update-statements"></a>處理 SELECT FOR UPDATE 陳述式
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 最大的互通性，應用程式應該產生結果集，將會藉由執行定位的 update 陳述式更新**選取用於更新**陳述式。 雖然資料指標程式庫不需要這個，它所需的大部分支援定位的 update 陳述式的資料來源。  
  
 資料指標程式庫會忽略中的資料行**FOR UPDATE**子句**SELECT FOR UPDATE**陳述式; 它會移除這個子句，再將該陳述式傳遞至驅動程式。 在資料指標程式庫，SQL_ATTR_CONCURRENCY 陳述式屬性，以及上一節中所述的限制中控制項的資料行中，將結果集中是否可以更新。
