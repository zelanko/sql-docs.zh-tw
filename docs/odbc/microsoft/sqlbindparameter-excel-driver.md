---
title: SQLBindParameter （Excel 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLBindParameter
- SQLBindParameter function [ODBC], Excel Driver
ms.assetid: 40489bc5-3e2a-425e-892d-e0dc037f4d7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b33200e0628566bc88f770ca1fe8fd895ecbf2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063247"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 當使用 Microsoft Excel 驅動程式時，執行使用參數將 Null 插入 SQL_CHAR 資料行中的 INSERT 語句，將會傳回具有 SQLSTATE 01004 的 SQL_SUCCESS_WITH_INFO 「資料已截斷」。
