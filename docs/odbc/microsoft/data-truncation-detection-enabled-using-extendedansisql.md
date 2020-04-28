---
title: 已使用 ExtendedAnsiSQL 啟用資料截斷偵測 |Microsoft Docs
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
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280693"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 啟用的資料截斷偵測
當 ExtendedAnsiSQL 旗標為開啟狀態，且應用程式將資料插入 char 或 binary 資料行中，並截斷資料時，將會偵測到截斷。 當 ExtendedAnsiSQL 旗標關閉時，資料會在不發出警告的情況下被截斷，如同舊版的 ODBC 桌面資料庫驅動程式一樣。
