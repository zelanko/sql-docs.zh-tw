---
title: SQLBindParameter （Excel 驅動程式） |Microsoft 文件
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
- Excel driver [ODBC], SQLBindParameter
- SQLBindParameter function [ODBC], Excel Driver
ms.assetid: 40489bc5-3e2a-425e-892d-e0dc037f4d7a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59af1eed7f5859db967b95f3d52e539d30ef6e62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32901593"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter （Excel 驅動程式）
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 使用 Microsoft Excel 驅動程式時，執行 SQL_CHAR 資料行中插入 null 值會使用參數的 INSERT 陳述式將會傳回 SQL_SUCCESS_WITH_INFO sqlstate 01004，「 資料 Truncated。 」
