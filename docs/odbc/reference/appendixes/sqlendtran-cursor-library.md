---
title: SQLEndTran(游標庫) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2277a67cd5410ea3c2a5d5b03b16d4533ed6ee1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304768"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLEndTran**函數。 有關**SQLEndTran**的一般資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
 游標庫不支援事務,並將對**SQLEndTran**的調用直接傳遞給驅動程式。 但是,游標庫確實支援數據源返回的帶有SQL_CURSOR_ROLLBACK_BEHAVIOR和SQL_CURSOR_COMMIT_BEHAVIOR資訊類型的游標提交和回滾行為:  
  
-   對於跨事務保留游標的數據源,在數據源中回滾的更改不會在游標庫的緩存中回滾。 要使緩存與資料源中的數據匹配,應用程式必須關閉並重新打開遊標。  
  
-   對於在事務邊界關閉游標的數據源,游標庫將關閉游標並刪除連接上所有語句的緩存。  
  
-   對於在事務邊界刪除已準備好的語句的數據源,應用程式必須在重新執行連接之前重新準備連接上的所有準備好的語句。
