---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 251ae0e4e94cec903e2c4b5cf687ed9b8b41dfc8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952393"
---
# <a name="identifiers-limitations"></a>識別碼限制
如果識別碼包含空格或特殊符號，則識別碼必須以反引號括住。 有效的名稱是不超過64個字元的字串，其中第一個字元不得為空格。 有效的名稱不能包含控制字元或下列特殊字元： ' &#124; # *？ [ ] . ! $ .  
  
 請不要在 ODBC 程式設計*人員參考*的附錄 C （也就是資料表或資料行名稱）中，使用 SQL 文法中所列的保留字，除非您將文字括在反向引號（'）中。
