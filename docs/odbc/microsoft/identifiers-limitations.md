---
title: 識別符限制 |微軟文件
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
ms.openlocfilehash: 7154f2db09b69e6376b1fe3af1de3f2c646ee94e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286248"
---
# <a name="identifiers-limitations"></a>識別碼限制
如果標識符包含空格或特殊符號,則必須在後引號中包含標識符。 有效名稱是不超過 64 個字元的字串,其中第一個字元不能是空格。 合法名稱不能包括控制字元或以下特殊字元:&#124; = * ? [ ] . ! $ .  
  
 請勿使用*ODBC 程式師參考*附錄 C 附錄 C 中列出的保留詞(或這些保留詞的速記形式)作為識別符(即表或列名稱),除非您在後引號 (『) 中環繞該單詞。
