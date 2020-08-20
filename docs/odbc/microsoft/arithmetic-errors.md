---
description: 算術錯誤
title: 算術錯誤 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2fa142b43f1e96693390f777c90ea6f10705f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500401"
---
# <a name="arithmetic-errors"></a>算術錯誤
ODBC 驅動程式會在提取每個資料列時，評估 SELECT 語句中的 WHERE 子句。 如果資料列包含導致算術錯誤的值，例如零除或數值溢位，驅動程式會傳回所有資料列，但會傳回有算術錯誤之資料行的錯誤。 但是，當您插入或更新時，ODBC 驅動程式會在第一次發生算術錯誤時停止插入或更新資料。
