---
title: SQLTables(Excel 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c436a1f52a862cda753d8c043515f5584607d98c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299298"
---
# <a name="sqltables-excel-driver"></a>SQLTables (Excel 驅動程式)
> [!NOTE]  
>  本主題提供特定於 Excel 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|引數|註解|  
|--------------|--------------|  
|*szTable 擁有者*|*szTableOwner*的唯一有效參數是 NULL,因為沒有任何驅動程式支援擁有者名稱。 將*szTableOwner*設定為 NULL 時,將傳回所有表。 NULL 在TABLE_OWNER列中返回。|  
|*szTable限定*|使用 Microsoft Excel 3.0 或 4.0 驅動程式時,如果調用**SQLTable**的值為*szTableQualifier,* 而不是現有表的名稱,則驅動程式將創建具有該名稱的表。<br /><br /> 在TABLE_QUALIFIER列中 **,SQLTables**將路徑傳回到目錄。|  
|*SzTable 類型*|對於 Microsoft Excel 3.0 或 4.0,"TABLE"是唯一支援的表類型。<br /><br /> 對於更高版本的 Microsoft Excel 檔,對於工作表名稱(末尾有"$"的表)返回"SYSTEM TABLE",對於工作表中的表返回"TABLE"。|
