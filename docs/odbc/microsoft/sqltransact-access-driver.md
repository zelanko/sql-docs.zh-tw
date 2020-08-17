---
description: SQLTransact (Access 驅動程式)
title: SQLTransact (Access 驅動程式) |Microsoft Docs
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
ms.openlocfilehash: 7e9b00f8f5a12af2d3823171d22ad53106569352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339666"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 使用 Microsoft Access 驅動程式時，對**SQLTransact**呼叫中的*fType*引數支援 SQL_COMMIT 和 SQL_ROLLBACK。  
  
 如果在認可程式期間發生失敗，則可以使用 Microsoft Access 驅動程式安裝程式中的 [修復資料庫] 選項，或在 **SQLConfigDataSource** 函式中使用 REPAIR_DB 關鍵字來修復受影響的資料庫。
