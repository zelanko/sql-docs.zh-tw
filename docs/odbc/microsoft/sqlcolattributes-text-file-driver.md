---
title: SQLColAttributes （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Text File Driver
ms.assetid: 132fd1c0-1921-4a7d-910e-aedf1bff5453
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bb242dcaf34f8fe7fad2886b13ddf5209c20c18
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855056"
---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|attribute|註解|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|SQL_COLUMN_DISPLAY_SIZE LONGVARBINARY 資料是資料行，而不 2 次的資料行的最大長度的最大長度。|  
|SQL_OWNER_NAME|空字串 ("") 會傳回此資料行中，因為不支援擁有者名稱。|  
|SQL_QUALIFIER_NAME|會傳回目錄的路徑。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 資料行報告為 SQL_UNSEARCHABLE。<br /><br /> 即使 LONGVARBINARY 和 LONGVARCHAR 不是，仍可供搜尋，固定長度和可變長度的二進位和字元資料類型。|
