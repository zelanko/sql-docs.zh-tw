---
title: SQLColumns （Paradox 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColumns
ms.assetid: d7831c7d-8be9-40a7-bc70-8d89db8fe8c9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 511059373ce5a464ac5f120ccd1c56bab63df6aa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolumns-paradox-driver"></a>SQLColumns （Paradox 驅動程式）
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|會傳回目錄的路徑。|  
|TABLE_OWNER|因為擁有者名稱不支援此資料行就會傳回 NULL。|  
|NULLABLE|SQL_NO_NULLS 參與的資料行就會傳回主索引鍵或唯一索引。|
