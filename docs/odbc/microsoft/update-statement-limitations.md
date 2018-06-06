---
title: UPDATE 陳述式的限制 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 006d0f9644c9f62a6b50e2d327384ec3a9c954c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="update-statement-limitations"></a>UPDATE 陳述式的限制
Paradox 驅動程式來更新資料表時，該資料表必須有唯一的索引 （Paradox 主索引鍵）。 當您使用 Paradox 驅動程式而不需要實作 Borland Database Engine 時，它不更新 Paradox 資料表。  
  
 不支援文字驅動程式。  
  
 使用 Microsoft Excel 驅動程式時，便可更新的值，但無法從 Microsoft Excel 試算表為基礎的資料表中刪除資料列。 如此一來，UPDATE 陳述式不是正式支援 Microsoft Excel 驅動程式。 INSERT 陳述式會視為受支援。
