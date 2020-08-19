---
description: SQLBindParameter (Excel 驅動程式)
title: SQLBindParameter (Excel 驅動程式) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f18d34bb17f6f6b039bac5f6842ff837c22f362
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483371"
---
# <a name="sqlbindparameter-excel-driver"></a>SQLBindParameter (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 使用 Microsoft Excel 驅動程式時，執行使用參數將 Null 插入 SQL_CHAR 資料行的 INSERT 語句，將會傳回具有 SQLSTATE 01004 「資料已截斷」的 SQL_SUCCESS_WITH_INFO。
