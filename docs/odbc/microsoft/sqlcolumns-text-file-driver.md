---
title: SQLColumns （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColumns
- SQLColumns function [ODBC], Text File Driver
ms.assetid: c99e5f8d-4e43-48f8-9e0e-086707b411f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8189a5f6a89f072988404e722a88c29af2d88ca6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829526"
---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|「資料行」|註解|  
|------------|--------------|  
|TABLE_QUALIFIER|會傳回目錄的路徑。|  
|TABLE_OWNER|在本專欄中會傳回 NULL，因為不支援擁有者名稱。|  
|NULLABLE|SQL_NO_NULLS 會傳回資料行參與主索引鍵或唯一索引中。|
