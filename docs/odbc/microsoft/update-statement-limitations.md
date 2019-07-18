---
title: UPDATE 陳述式限制 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088198"
---
# <a name="update-statement-limitations"></a>UPDATE 陳述式限制
Paradox 驅動程式更新的資料表，資料表必須有唯一的索引 （Paradox 主索引鍵）。 當您使用 Paradox 驅動程式，而不需要實作 Borland 資料庫引擎時，它不可以更新 Paradox 資料表。  
  
 不支援文字驅動程式。  
  
 使用 Microsoft Excel 驅動程式時，就可以更新的值，但無法從 Microsoft Excel 試算表為基礎的資料表中刪除資料列。 如此一來，UPDATE 陳述式不視為正式支援的 Microsoft Excel 驅動程式。 INSERT 陳述式會視為受支援。
