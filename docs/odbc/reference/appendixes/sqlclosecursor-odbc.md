---
title: SQLCloseCursor_ODBC |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1b61267d093e11bf7ea25158f5dc6a29ccba6a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296298"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLCloseCursor**函數。 有關**SQLCloseCursor 的**一般資訊,請參閱[SQLCloseCursor 函數](../../../odbc/reference/syntax/sqlclosecursor-function.md)。  
  
 沒有打開的游標,遊標庫不支援調用**SQLCloseCursor。** 嘗試此將返回 SQLSTATE 24000(無效游標狀態)。 在未打開遊標時,使用SQL_CLOSE*選項*調用**SQLFreeStmt,** 游標庫支援。
