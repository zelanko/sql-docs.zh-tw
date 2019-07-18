---
title: SQLColAttributes （Access 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c78229da8a577670ba31ae82c679bfefbef4f80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903984"
---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|屬性|註解|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|SQL_COLUMN_DISPLAY_SIZE LONGVARBINARY 資料是資料行，而不 2 次的資料行的最大長度的最大長度。|  
|SQL_OWNER_NAME|空字串 ("") 會傳回此資料行中，因為不支援擁有者名稱。|  
|SQL_QUALIFIER_NAME|會傳回資料庫檔案的路徑。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 資料行報告為 SQL_UNSEARCHABLE。<br /><br /> 即使 LONGVARBINARY 和 LONGVARCHAR 不是，仍可供搜尋，固定長度和可變長度的二進位和字元資料類型。|  
  
> [!NOTE]  
>  上述不是所傳回的屬性完整清單**SQLColAttributes**。
