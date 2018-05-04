---
title: 識別項限制 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 591404db64ec5969b1236c318984191caea3a2cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="identifiers-limitations"></a>識別項限制
如果識別項包含空格或特殊符號，識別項必須括在後引號中。 有效的名稱是不超過 64 個字元，其中的第一個字元必須不是空格的字串。 有效的名稱不能包含控制字元或下列特殊字元: ' &#124; # *？ [ ] . ! $ .  
  
 請勿的使用 SQL 文法中的 < 附錄 C 中所列的保留的字*ODBC 程式設計人員參考*（或這些保留字的簡短形式） 作為識別項 （也就是資料表或資料行名稱），除非您圍繞 word 在上一步引號 （'）。
