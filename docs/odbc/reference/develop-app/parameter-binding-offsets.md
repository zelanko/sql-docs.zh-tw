---
description: 參數繫結位移
title: 參數系結位移 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71b4958e77d01c613e33386ec1b2b21ed91f0a67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476540"
---
# <a name="parameter-binding-offsets"></a>參數繫結位移
應用程式可以指定在呼叫 **SQLExecDirect** 或 **SQLExecute** 時，將位移加入至系結的參數緩衝區位址，以及對應的長度/指標緩衝區位址。 這些新增專案的結果會決定這些作業中使用的位址。  
  
 系結位移可讓應用程式變更系結，而不需要針對先前系結的參數呼叫 **SQLBindParameter** 。 呼叫 **SQLBindParameter** 來重新系結參數會變更緩衝區位址和長度/指標指標。 另一方面，使用位移進行重新系結，只會將位移加入至現有的系結參數緩衝區位址和長度/指標緩衝區位址。 使用位移時，系結是應用程式緩衝區配置方式的「範本」，而應用程式可以藉由變更位移來將此「範本」移至不同的記憶體區域。 您可以隨時指定新的位移，且一律會新增至原始系結的值。  
  
 為了指定系結位移，此應用程式會將 SQL_ATTR_PARAM_BIND_OFFSET_PTR 語句屬性設定為 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用系結的函式之前，只要參數緩衝區位址或長度/指標緩衝區位址都不是0，而且系結參數在 SQL 語句中，就會在這個緩衝區中以位元組為單位來放置位移。 位址和位移的總和必須是有效的位址。  (這表示，只要或兩者的總和是有效的位址，就會將位移和加入位移的位址設為無效。 )   
  
> [!NOTE]  
>  ODBC 2 不支援系結位移。*x* 驅動程式。
