---
title: SQLTables （Paradox 驅動程式） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299282"
---
# <a name="sqltables-paradox-driver"></a>SQLTables (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|引數|評價|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*的唯一有效引數為 Null，因為沒有任何驅動程式支援擁有者名稱。 當*szTableOwner*設為 Null 時，就會傳回所有資料表。 TABLE_OWNER 資料行中傳回 Null。|  
|*szTableQualifier*|在 [TABLE_QUALIFIER] 資料行中， **SQLTables**會傳回目錄的路徑。|  
|*SzTableType*|若是 Paradox 檔案，"TABLE" 是唯一支援的資料表類型。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLTables 函式](../../odbc/reference/syntax/sqltables-function.md)
