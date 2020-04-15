---
title: 狀態轉換檢查 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dc1ddc126a2d652dfdb038cbb0e510f9735d7b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299703"
---
# <a name="state-transition-checks"></a>狀態轉換檢查
驅動程式管理員檢查環境、連接或語句的狀態是否適合被調用的函數。 例如,在調用**SQLConnect**時,連接必須處於分配狀態;調用**SQLExecute**時,語句必須處於準備狀態。 驅動程式管理員返回SQL_ERROR狀態轉換錯誤。
