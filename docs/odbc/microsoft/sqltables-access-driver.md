---
title: SQLTables （Access 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3a23af365efbef6a0f0da2c52568501425ecb3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306089"
---
# <a name="sqltables-access-driver"></a>SQLTables (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|引數|評價|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*的唯一有效引數為 Null，因為沒有任何驅動程式支援擁有者名稱。 當*szTableOwner*設為 Null 時，就會傳回所有資料表。 TABLE_OWNER 資料行中傳回 Null。|  
|*szTableQualifier*|在 [TABLE_QUALIFIER] 資料行中， **SQLTables**會傳回資料庫檔案的路徑。|  
|*SzTableType*|使用 Microsoft Access 驅動程式時，系統資料表的*szTableType*支援「系統資料表」，附加資料表支援「同義字」，而且資料列傳回查詢支援「VIEW」。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLTables 函式](../../odbc/reference/syntax/sqltables-function.md)
