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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7fb67171a796755bf8d6229b9d562f69bd588ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096514"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 啟用的資料截斷偵測
當 ExtendedAnsiSQL 旗標為開啟狀態，且應用程式將資料插入 char 或 binary 資料行中，並截斷資料時，將會偵測到截斷。 當 ExtendedAnsiSQL 旗標關閉時，資料會在不發出警告的情況下被截斷，如同舊版的 ODBC 桌面資料庫驅動程式一樣。
