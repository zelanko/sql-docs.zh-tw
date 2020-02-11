---
title: 狀態轉換檢查 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b337d317092ad6ae20cc91236d69c1314de96bce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107277"
---
# <a name="state-transition-checks"></a>狀態轉換檢查
驅動程式管理員會檢查環境、連接或語句的狀態是否適用于所呼叫的函式。 例如，當呼叫**SQLConnect**時，連接必須處於已配置的狀態;呼叫**SQLExecute**時，語句必須處於準備狀態。 驅動程式管理員會傳回狀態轉換錯誤的 SQL_ERROR。
