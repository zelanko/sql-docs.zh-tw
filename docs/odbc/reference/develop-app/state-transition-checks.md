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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dc1ddc126a2d652dfdb038cbb0e510f9735d7b0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299703"
---
# <a name="state-transition-checks"></a>狀態轉換檢查
驅動程式管理員會檢查環境、連接或語句的狀態是否適用于所呼叫的函式。 例如，當呼叫**SQLConnect**時，連接必須處於已配置的狀態;呼叫**SQLExecute**時，語句必須處於準備狀態。 驅動程式管理員會傳回狀態轉換錯誤的 SQL_ERROR。
