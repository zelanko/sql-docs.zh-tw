---
title: SQLRowCount(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9fe597f54ecb4bc82439251e2228ac5fdc4ea3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300588"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLRowCount**函數。 有關**SQLRowCount 的一**般資訊,請參閱[SQLRowCount 函數](../../../odbc/reference/syntax/sqlrowcount-function.md)。  
  
 當應用程式使用與游標關聯的語句調用**SQLRowCount**時,遊標庫返回從驅動程式檢索到的數據行數。  
  
 當應用程式使用與定位更新或刪除語句關聯的語句調用**SQLRowCount**時,遊標庫返回受該語句影響的行數。  
  
 當應用程式在**SELECT**語句後調用**SQLRowCount**時,遊標庫返回 -1。
