---
title: SQLTransact （存取驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aeed0fc0d6bb19c7440c35f39094c05bf17bfbf7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqltransact-access-driver"></a>SQLTransact （存取驅動程式）
> [!NOTE]  
>  本主題提供存取驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 使用 Microsoft Access 驅動程式時，支援 SQL_COMMIT 和 SQL_ROLLBACK 如*fType*呼叫中的引數**SQLTransact**。  
  
 如果您在認可程序期間發生失敗，可以透過修復資料庫選項，在 Microsoft Access 驅動程式安裝程式，或使用中的 REPAIR_DB 關鍵字修復受影響的資料庫**SQLConfigDataSource**函式。
