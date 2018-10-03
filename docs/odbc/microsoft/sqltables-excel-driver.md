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
manager: craigg
ms.openlocfilehash: 23ce67350b7fa7d0a88f3d51e618ce9bb9f9ebcf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796216"
---
# <a name="sqltables-excel-driver"></a>SQLTables (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|引數|註解|  
|--------------|--------------|  
|*szTableOwner*|唯一有效的引數，如*szTableOwner*是 NULL，因為沒有任何驅動程式支援擁有者名稱。 具有*szTableOwner*設為 NULL，會傳回所有資料表。 TABLE_OWNER 資料行就會傳回 NULL。|  
|*szTableQualifier*|Microsoft Excel 3.0 或 4.0 版的驅動程式使用時，如果您呼叫**SQLTables**具有值*szTableQualifier* ，不是現有資料表的名稱、 驅動程式會建立具有該名稱的資料表。<br /><br /> 在 TABLE_QUALIFIER 欄中， **SQLTables**會傳回目錄的路徑。|  
|*SzTableType*|Microsoft Excel 3.0 或 4.0，「 資料表 」 會是唯一支援的資料表類型。<br /><br /> 較新版的 Microsoft Excel 檔案的詳細資訊，工作表名稱 （以"$"端的資料表），會傳回 「 系統資料表 」 以及 「 資料表 」 會傳回工作表內的資料表。|
