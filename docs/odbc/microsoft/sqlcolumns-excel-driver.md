---
description: SQLColumns (Excel 驅動程式)
title: SQLColumns (Excel 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Excel Driver
- Excel driver [ODBC], SQLColumns
ms.assetid: 4bae3fcd-0287-4f79-ad7c-8f7ab2f6f940
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b44c3ee23eead3f2798c2389e66f82d77f48cc1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412054"
---
# <a name="sqlcolumns-excel-driver"></a>SQLColumns (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
|資料行|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|傳回目錄的路徑。|  
|TABLE_OWNER|因為不支援擁有者名稱，所以會在此資料行中傳回 Null。|  
|NULLABLE|對於參與主鍵或唯一索引的資料行，會傳回 SQL_NO_NullS。|
