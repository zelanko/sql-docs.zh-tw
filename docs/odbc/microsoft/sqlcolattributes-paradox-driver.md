---
title: SQLColAttributes （Paradox 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColAttributes
ms.assetid: bbeef024-d470-4d28-b61b-26997ef41007
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9b7d5967108d605d6b7426dcd662507a49037108
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132672"
---
# <a name="sqlcolattributes-paradox-driver"></a>SQLColAttributes (Paradox 驅動程式)
> [!NOTE]  
>  本主題提供 Paradox 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|屬性|註解|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|SQL_COLUMN_DISPLAY_SIZE LONGVARBINARY 資料是資料行，而不 2 次的資料行的最大長度的最大長度。|  
|SQL_OWNER_NAME|空字串 ("") 會傳回此資料行中，因為不支援擁有者名稱。|  
|SQL_QUALIFIER_NAME|會傳回目錄的路徑。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 資料行報告為 SQL_UNSEARCHABLE。<br /><br /> 即使 LONGVARBINARY 和 LONGVARCHAR 不是，仍可供搜尋，固定長度和可變長度的二進位和字元資料類型。|  
  
> [!NOTE]  
>  上述不是所傳回的屬性完整清單**SQLColAttributes**。
