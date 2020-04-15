---
title: 建立索引語句 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280968"
---
# <a name="create-index-statement"></a>CREATE INDEX 陳述式
CREATE INDEX 語句的語法是:  
  
 在*表名*上建立 [唯一]*索引名稱*(*列標識符*[ASC][DESC],*列標識符*[ASC][DESC]...)以\<*索引選項清單*>  
  
 \<*索引選項清單*>可以是:主&#124;無效 &#124;忽略 NULL  
  
 只有 Microsoft Access 驅動程式使用「無效」和「忽略」空索引選項。 dBASE 和 Paradox 驅動程式接受語法,但忽略任一選項的存在。  
  
 使用悖論驅動程式時,CREATE INDEX 語句將創建 Paradox 主鍵檔和輔助檔。  
  
 Microsoft Excel 或文本驅動程式不支援此語句。
