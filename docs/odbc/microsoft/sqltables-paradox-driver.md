---
title: SQLTables(悖論驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa13b5395d8f3c2cb470a4eff1b1ef02a43bad53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299282"
---
# <a name="sqltables-paradox-driver"></a>SQLTables (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供特定於悖論驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|引數|註解|  
|--------------|--------------|  
|*szTable 擁有者*|*szTableOwner*的唯一有效參數是 NULL,因為沒有任何驅動程式支援擁有者名稱。 將*szTableOwner*設定為 NULL 時,將傳回所有表。 NULL 在TABLE_OWNER列中返回。|  
|*szTable限定*|在TABLE_QUALIFIER列中 **,SQLTables**將路徑傳回到目錄。|  
|*SzTable 類型*|對於 Paradox 檔案,"TABLE"是唯一支援的表類型。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLTables 函式](../../odbc/reference/syntax/sqltables-function.md)
