---
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
ms.openlocfilehash: ab1b472540d1978a6e7a06d94da7542cc641e999
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299898"
---
# <a name="arithmetic-errors"></a>算術錯誤
ODBC 驅動程式會在提取每個資料列時，評估 SELECT 語句中的 WHERE 子句。 如果資料列包含導致算術錯誤的值（例如零除或數值溢位），驅動程式會傳回所有資料列，但會傳回具有算術錯誤之資料行的錯誤。 不過，在插入或更新時，ODBC 驅動程式會在遇到第一個算術錯誤時停止插入或更新資料。
