---
title: SQLTables （Excel 驅動程式） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 89157178aa9c134bdb1b9518343007adb1e1e05f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132418"
---
# <a name="sqltables-excel-driver"></a>SQLTables (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*的唯一有效引數為 Null，因為沒有任何驅動程式支援擁有者名稱。 當*szTableOwner*設為 Null 時，就會傳回所有資料表。 TABLE_OWNER 資料行中傳回 Null。|  
|*szTableQualifier*|使用 Microsoft Excel 3.0 或4.0 驅動程式時，如果您以不是現有資料表名稱的*szTableQualifier*值呼叫**SQLTables** ，驅動程式將會建立具有該名稱的資料表。<br /><br /> 在 [TABLE_QUALIFIER] 資料行中， **SQLTables**會傳回目錄的路徑。|  
|*SzTableType*|針對 Microsoft Excel 3.0 或4.0，"TABLE" 是唯一支援的資料表類型。<br /><br /> 若為較新版本的 Microsoft Excel 檔案，則會傳回工作表名稱的「系統資料表」（結尾有 "$" 的資料表），並針對工作表內的資料表傳回 "TABLE"。|
