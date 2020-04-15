---
title: VARCHAR 欄位大小(Oracle 的 ODBC 驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304823"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>VARCHAR 資料行大小 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 在 Oracle8 中,VARCHAR 列的最大大小從 2000 位元組增加到 4000 位元組。 Oracle 7.3.x 用戶端軟體無法綁定大於 2000 位元組的參數值。 因此,如果創建 VARCHAR 列大於 2000 位元組的表,則無法對它執行參數化插入、更新、刪除和查詢,數據超過用戶端軟體的 2000 位元組限制。 由於 Oracle 的 ODBC 驅動程式和 Oracle 的 OLE DB 提供程式都使用參數化插入、更新、刪除和查詢,因此在這種情況下,它們將報告 ORA-01026 錯誤。 在 Oracle 客戶端軟體強制執行的限制範圍內的數據將起作用。 為了避免此 2000 位元組限制,必須將用戶端軟體升級到 Oracle8(8.0.4.1.1c 或更高版本)。
