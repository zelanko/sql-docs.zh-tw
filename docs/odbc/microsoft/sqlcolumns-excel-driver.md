---
title: SQLColumns （Excel 驅動程式） |Microsoft Docs
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
ms.openlocfilehash: c168168e0cb44d6aff2102bb18c07cbf1a1953a5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307879"
---
# <a name="sqlcolumns-excel-driver"></a>SQLColumns (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|資料行|評價|  
|------------|--------------|  
|TABLE_QUALIFIER|會傳回目錄的路徑。|  
|TABLE_OWNER|此資料行中會傳回 Null，因為不支援擁有者名稱。|  
|NULLABLE|針對參與 primary key 或 unique 索引的資料行，會傳回 SQL_NO_NullS。|
