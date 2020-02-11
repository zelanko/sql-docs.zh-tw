---
title: SQLTransact （Access 驅動程式） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4d4b3d8d417591bd72dde22240c81a91d80f990
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948977"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 使用 Microsoft Access 驅動程式時，在呼叫**SQLTransact**的*fType*引數中支援 SQL_COMMIT 和 SQL_ROLLBACK。  
  
 如果在認可過程中發生失敗，則可以使用 Microsoft Access 驅動程式設定中的 [修復資料庫] 選項來修復受影響的資料庫，或透過在**SQLConfigDataSource**函式中使用 REPAIR_DB 關鍵字來進行修復。
