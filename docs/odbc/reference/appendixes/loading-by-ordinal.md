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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64bff8dcdd3802f75dc402c9ada60f82580aca5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288718"
---
# <a name="loading-by-ordinal"></a>依序數載入
在 ODBC *2.x 中，* 可以執行以序數來載入，以改善連接程式的效能。 *ODBC 2.x*驅動程式會匯出具有序數199的虛擬函式。當驅動程式管理員偵測到它時，它會依序數（而不是依名稱）解析 ODBC 函式的位址。 ODBC 2.x 驅動程式仍然支援這種功能，*但 odbc 3.x* *驅動程式並*不支援。
