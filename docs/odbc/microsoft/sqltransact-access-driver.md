---
title: SQLTransact(存取驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f88d3154925ab589a8519cb9205da03e8c3dc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299260"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Access 驅動程式)
> [!NOTE]  
>  本主題提供特定於訪問驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 使用 Microsoft Access 驅動程式時,fType 參數在調用**SQLTransact**中支援*fType*參數SQL_COMMIT和SQL_ROLLBACK。  
  
 如果在提交過程中發生故障,可以使用 Microsoft Access 驅動程式設置中的修復資料庫選項,或者透過使用**SQLConfigDataSource**函數中的REPAIR_DB關鍵字來修復受影響的資料庫。
