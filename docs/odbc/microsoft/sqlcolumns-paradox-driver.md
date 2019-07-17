---
title: SQLColumns （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColumns
ms.assetid: d7831c7d-8be9-40a7-bc70-8d89db8fe8c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1738e17742e61a285a4d2d070b179d2832aaf40f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132505"
---
# <a name="sqlcolumns-paradox-driver"></a>SQLColumns (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|「資料行」|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|會傳回目錄的路徑。|  
|TABLE_OWNER|在本專欄中會傳回 NULL，因為不支援擁有者名稱。|  
|NULLABLE|SQL_NO_NULLS 會傳回資料行參與主索引鍵或唯一索引中。|
