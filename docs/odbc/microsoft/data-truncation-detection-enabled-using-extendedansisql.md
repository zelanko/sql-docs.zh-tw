---
description: 使用 ExtendedAnsiSQL 啟用的資料截斷偵測
title: 使用 ExtendedAnsiSQL 啟用的資料截斷偵測 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26965093caecbc11e94ef738ba6b8ff757b43258
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412886"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 啟用的資料截斷偵測
當開啟 ExtendedAnsiSQL 旗標，且應用程式將資料插入 char 或 binary 資料行，且資料遭到截斷時，將會偵測到截斷。 關閉 ExtendedAnsiSQL 旗標時，資料會被截斷而不發出警告，如同舊版 ODBC Desktop 資料庫驅動程式一樣。
