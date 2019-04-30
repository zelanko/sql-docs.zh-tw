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
manager: craigg
ms.openlocfilehash: c781113124d456e1ba866546d6ada7a17371d71f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208523"
---
# <a name="identifiers-limitations"></a>識別碼限制
如果識別碼包含空格或特殊符號，識別項必須加上後引號括住。 有效的名稱是不能超過 64 個字元，其中的第一個字元必須不是空格的字串。 有效的名稱不能包含控制字元或下列特殊字元: ' &#124; # *？ [ ] . ! $ .  
  
 請勿的使用保留的字列在 SQL 文法中的 < 附錄 C *ODBC 程式設計人員參考*（或這些保留字的簡短形式） 做為識別項 （也就是資料表或資料行名稱），除非括住文字後方引號 （'）。
