---
title: UPDATE 語句限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cc8cf58d4e4d826dc4b152e395dedbea395a095
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088198"
---
# <a name="update-statement-limitations"></a>UPDATE 陳述式限制
若要讓 Paradox 驅動程式更新資料表，資料表必須有唯一的索引（Paradox 主鍵）。 當您使用 Paradox 驅動程式，但未執行 Borland 資料庫引擎時，就不可能更新 Paradox 資料表。  
  
 文字驅動程式不支援。  
  
 使用 Microsoft Excel 驅動程式時，可以更新值，但無法從以 Microsoft Excel 試算表為基礎的資料表中刪除資料列。 因此，Microsoft Excel 驅動程式不會將 UPDATE 語句視為正式支援。 只會將 INSERT 語句視為受支援。
