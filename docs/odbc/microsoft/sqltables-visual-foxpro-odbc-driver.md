---
description: SQLTables (Visual FoxPro ODBC Driver)
title: SQLTables (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 089208ab612984283e3f87c4ad03aca0ccfa2b38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471550"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級1  
  
 傳回 **SQLTables** 語句中參數所指定的資料表名稱清單。 如果未指定任何參數，則會傳回儲存在目前資料來源中的資料表名稱。 驅動程式會以結果集的形式傳回信息。  
  
 列舉型別呼叫將不會收到遠端視圖或本機參數化視圖的結果集專案。 不過，使用唯一的資料表名稱規範來呼叫 **SQLTables** 時，會找到與該名稱相符的這類視圖：這可讓您在建立新的資料表之前，使用 API 來檢查名稱衝突。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驅動程式會區分 [資料庫資料表](../../odbc/microsoft/visual-foxpro-terminology.md) 和 [可用資料表](../../odbc/microsoft/visual-foxpro-terminology.md)，即使這兩種類型的資料表都儲存在您系統上的相同目錄中。 如果您的資料來源是可用資料表的目錄，則 Visual FoxPro ODBC 驅動程式不會目錄或傳回與資料庫相關聯之任何資料表的名稱。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLTables](../../odbc/reference/syntax/sqltables-function.md) 。
