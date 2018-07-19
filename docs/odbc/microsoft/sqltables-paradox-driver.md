---
title: SQLTables （Paradox 驅動程式） |Microsoft 文件
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
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1108b06702a4753f0f99f6e67418fe8f54dc7de8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904083"
---
# <a name="sqltables-paradox-driver"></a>SQLTables （Paradox 驅動程式）
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|唯一有效的引數，如*szTableOwner*是 NULL，因為沒有驅動程式支援擁有者名稱。 與*szTableOwner*設為 NULL，會傳回所有資料表。 TABLE_OWNER 資料行就會傳回 NULL。|  
|*szTableQualifier*|TABLE_QUALIFIER 資料行中**SQLTables**會傳回路徑的目錄。|  
|*SzTableType*|Paradox 檔案的"TABLE"會是唯一支援的資料表類型。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLTables 函式](../../odbc/reference/syntax/sqltables-function.md)
