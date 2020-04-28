---
title: VARCHAR 資料行大小（ODBC Driver for Oracle） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e1de3171521c57c80beb207d33e67d26d3e33
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304823"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 資料行大小 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 在 Oracle8 中，VARCHAR 資料行的大小上限已從2000增加至4000個位元組。 Oracle 7.3. x 用戶端軟體無法系結大於2000個位元組的參數值。 因此，如果您建立的資料表具有大於2000個位元組的 VARCHAR 資料行，您將無法對其執行參數化的插入、更新、刪除和查詢，其資料會超過用戶端軟體的2000位元組限制。 由於適用于 Oracle 的 ODBC 驅動程式和 Oracle 的 OLE DB 提供者都會使用參數化插入、更新、刪除和查詢，因此在此情況下，它們會報告 TNSNAMES.ORA-01026 錯誤。 Oracle 用戶端軟體所強制執行之限制內的資料將會生效。 若要避免這個2000位元組的限制，您必須將用戶端軟體升級至 Oracle8 （8.0.4.1.1 c 或更高版本）。
