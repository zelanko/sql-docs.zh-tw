---
title: 處理更新敘述的選擇 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308009"
---
# <a name="processing-select-for-update-statements"></a>處理 SELECT FOR UPDATE 陳述式
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 為了達到最大的互操作性,應用程式應生成結果集,這些結果集將通過執行**SELECT FOR 更新**語句來使用定位的更新語句進行更新。 儘管游標庫不需要這樣做,但大多數支援定位更新語句的數據源都需要它。  
  
 游標庫忽略"選擇更新"語句的**FOR 更新**子句中的列;因此,遊標庫將忽略"**選擇更新"** 語句中的列。在將語句傳遞給驅動程式之前,它會刪除此子句。 在游標庫中,SQL_ATTR_CONCURRENCY語句屬性以及上一節中提及的限制控制是否可以更新結果集中的列。
