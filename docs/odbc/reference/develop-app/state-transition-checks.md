---
description: 狀態轉換檢查
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
ms.openlocfilehash: 50a845f2b83ada7c9d4f03f252b6d2bc3d3eff3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476370"
---
# <a name="state-transition-checks"></a>狀態轉換檢查
驅動程式管理員會檢查環境、連接或語句的狀態是否適用于被呼叫的函式。 例如，呼叫 **SQLConnect** 時，連接必須處於已配置狀態;呼叫 **SQLExecute** 時，語句必須處於已備妥的狀態。 驅動程式管理員會傳回狀態轉換錯誤的 SQL_ERROR。
