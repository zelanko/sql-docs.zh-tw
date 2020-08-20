---
description: 識別碼限制
title: 識別碼限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5efaba8fa73f61082be8d7cd8dca78626a9f972
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500341"
---
# <a name="identifiers-limitations"></a>識別碼限制
如果識別碼包含空格或特殊的符號，則識別碼必須用引號括住。 有效的名稱是不超過64個字元的字串，其中第一個字元不得為空格。 有效的名稱不能包含控制字元或下列特殊字元： ' &#124; # *？ [ ] . ! $ .  
  
 請勿使用 ODBC 程式設計師 *參考* (的附錄 C 中所列的保留字，或這些保留字的速記形式) 做為識別碼 (也就是) 的資料表或資料行名稱，除非您將引號括在反向引號 (') 中。
