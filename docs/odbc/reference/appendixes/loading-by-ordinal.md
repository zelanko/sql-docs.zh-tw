---
title: 依序數載入 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fdc7728fe06df708efd973423f5c8c05333ce189
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041597"
---
# <a name="loading-by-ordinal"></a>依序數載入
在 ODBC *2.x*，無法執行依序數載入，以改善連線程序的效能。 ODBC *2.x*驅動程式匯出序數 199 虛擬函式; 當驅動程式管理員偵測到它，序數，而不使用名稱解析的 ODBC 函式的位址。 這項功能仍支援適用於 ODBC *2.x*驅動程式，但不是支援適用於 ODBC *3.x*驅動程式。
