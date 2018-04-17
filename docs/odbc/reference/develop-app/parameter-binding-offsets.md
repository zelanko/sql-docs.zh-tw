---
title: 參數繫結位移 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d5228c7ce920eb56b0b947784b3d5a7bb2d6266
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="parameter-binding-offsets"></a>參數繫結位移
應用程式可以指定位移，加入繫結參數緩衝區位址和對應的長度/指標緩衝區位址時**SQLExecDirect**或**SQLExecute**呼叫。 這些加入作業的結果判斷這些作業中使用的位址。  
  
 繫結位移允許應用程式變更繫結，而不需呼叫**SQLBindParameter**先前繫結參數。 呼叫**SQLBindParameter**重新繫結參數變更緩衝區位址和長度/指標的指標。 重新繫結的位移，相反地，只要將位移新增至現有的繫結的參數緩衝區位址和長度/指標緩衝區位址。 當使用位移時，繫結就是 「 範本 」 的應用程式緩衝區的配置方式，應用程式可以藉由變更位移到不同的記憶體區域中移這個 「 範本 」。 隨時都可以指定新的位移，並永遠會加入到原始繫結的值。  
  
 若要指定繫結位移，應用程式會將 SQL_ATTR_PARAM_BIND_OFFSET_PTR 陳述式屬性設定 SQLINTEGER 緩衝區的位址。 應用程式呼叫的函式會使用繫結之前，就會將位移 （位元組），這個緩衝區中，只要參數緩衝區位址和長度/指標緩衝區位址都不是 0，而繫結的參數是 SQL 陳述式中。 位址和位移的總和必須是有效的位址。 （這表示，或兩個位移與位移加入的位址可以是無效的只要其總和會是有效的位址）。  
  
> [!NOTE]  
>  ODBC 2 不支援繫結的位移。*x*驅動程式。
