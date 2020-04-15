---
title: 按 Ordinal 載入 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288718"
---
# <a name="loading-by-ordinal"></a>依序數載入
在 ODBC *2.x*中,可以執行序號載入以提高連接過程的性能。 ODBC *2.x*驅動程式匯出帶有假函數的虛擬函數 199;當驅動程式管理員檢測到它時,它按位數而不是名稱解析 ODBC 函數的位址。 ODBC *2.x*驅動程式仍然支援此功能,但 ODBC *3.x*驅動程式不支援此功能。
