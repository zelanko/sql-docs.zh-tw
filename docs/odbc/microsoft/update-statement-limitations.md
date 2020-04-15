---
title: 更新語句限制 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307619"
---
# <a name="update-statement-limitations"></a>UPDATE 陳述式限制
要更新表,表必須具有唯一索引(悖論主鍵)。 當您在不實現 Borland 資料庫引擎的情況下使用悖論驅動程式時,無法更新 Paradox 表。  
  
 文本驅動程式不支援。  
  
 使用 Microsoft Excel 驅動程式時,可以更新值,但不能從基於 Microsoft Excel 電子表格的表中刪除行。 因此,Microsoft Excel 驅動程式不認為 UPDATE 語句不受官方支援。 只有 INSERT 語句被視為受支援。
