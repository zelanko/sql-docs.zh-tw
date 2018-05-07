---
title: SQLTables （Excel 驅動程式） |Microsoft 文件
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
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2921d9e047e03cae092e5c0e7d2fcd4e4f8f24c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqltables-excel-driver"></a>SQLTables （Excel 驅動程式）
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|唯一有效的引數，如*szTableOwner*是 NULL，因為沒有驅動程式支援擁有者名稱。 與*szTableOwner*設為 NULL，會傳回所有資料表。 TABLE_OWNER 資料行就會傳回 NULL。|  
|*szTableQualifier*|Microsoft Excel 3.0 或 4.0 版的驅動程式使用時，如果您呼叫**SQLTables**使用值為*szTableQualifier* ，不是現有資料表的名稱，此驅動程式會建立具有該名稱的資料表。<br /><br /> TABLE_QUALIFIER 資料行中**SQLTables**會傳回路徑的目錄。|  
|*SzTableType*|Microsoft Excel 3.0 或 4.0，「 資料表 」 是唯一支援的資料表類型。<br /><br /> 對於新版的 Microsoft Excel 檔案中，工作表名稱 （以"$"結尾上的資料表），就會傳回 「 系統資料表 」 和 「 資料表 」 會傳回工作表內的資料表。|
