---
title: "SQLColAttributes （文字檔案驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Text File Driver
ms.assetid: 132fd1c0-1921-4a7d-910e-aedf1bff5453
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 811ccdff731e006d1ee112674b47531573778354
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes （文字檔案驅動程式）
> [!NOTE]  
>  本主題提供文字檔驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|Attribute|註解|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|SQL_COLUMN_DISPLAY_SIZE LONGVARBINARY 資料是資料行，而不時間 2 的資料行的最大長度的最大長度。|  
|SQL_OWNER_NAME|空字串 ("") 不支援擁有者名稱，因此，會傳回此資料行中。|  
|SQL_QUALIFIER_NAME|會傳回目錄的路徑。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY 和 LONGVARCHAR 資料行報告為 SQL_UNSEARCHABLE。<br /><br /> 雖然 LONGVARBINARY 和 LONGVARCHAR 不是，仍可搜尋，固定長度和可變長度的二進位和字元資料類型。|

