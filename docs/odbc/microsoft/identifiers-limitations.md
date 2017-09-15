---
title: "識別項限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ec32697030d2ad4ede765879f83956692ed49914
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="identifiers-limitations"></a>識別項限制
如果識別項包含空格或特殊符號，識別項必須括在後引號中。 有效的名稱是不超過 64 個字元，其中的第一個字元必須不是空格的字串。 有效的名稱不能包含控制字元或下列特殊字元: ' &#124;# * ? [ ] . ! $ .  
  
 請勿的使用 SQL 文法中的 < 附錄 C 中所列的保留的字*ODBC 程式設計人員參考*（或這些保留字的簡短形式） 作為識別項 （也就是資料表或資料行名稱），除非您圍繞 word 在上一步引號 （'）。
