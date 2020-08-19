---
description: 依序數載入
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb8929962e97e7560f50117218f621cd21846fc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429630"
---
# <a name="loading-by-ordinal"></a>依序數載入
在 ODBC *2.x 中，* 可以執行依序數載入，以改善連接處理常式的效能。 *ODBC 2.x*驅動程式會匯出具有序數199的虛函數;當驅動程式管理員偵測到它時，它會依序數解析 ODBC 函式的位址，而不是依名稱。 ODBC 2.x 驅動程式仍然支援這項功能，*但是 odbc 3.x* *驅動程式不*支援此功能。
