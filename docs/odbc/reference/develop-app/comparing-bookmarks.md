---
description: 比較書籤
title: 比較書簽 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 939c3780fc9c6738a307e9a969a346951cfac5e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476780"
---
# <a name="comparing-bookmarks"></a>比較書籤
因為書簽可進行位元組比較，所以可以比較是否相等或不等。 若要這樣做，應用程式會將每個書簽視為位元組陣列，並比較兩個書簽（以位元組為單位）。 因為書簽保證只在結果集中不同，所以比較從不同結果集取得的書簽並不合理。
