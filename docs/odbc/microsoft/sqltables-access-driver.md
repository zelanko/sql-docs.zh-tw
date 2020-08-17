---
description: SQLTables (Access 驅動程式)
title: SQLTables (Access 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 69dce4116064cdb7509f628fcc493e57c414666e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339914"
---
# <a name="sqltables-access-driver"></a>SQLTables (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*唯一有效的引數為 Null，因為沒有任何驅動程式支援擁有者名稱。 當 *szTableOwner* 設定為 Null 時，就會傳回所有資料表。 TABLE_OWNER 資料行中會傳回 Null。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 資料行中， **SQLTables** 會傳回資料庫檔案的路徑。|  
|*SzTableType*|使用 Microsoft Access 驅動程式時，系統資料表的 *szTableType* 支援「系統資料表」、附加資料表支援「同義字」，且資料列傳回查詢支援「視圖」。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLTables 函式](../../odbc/reference/syntax/sqltables-function.md)
