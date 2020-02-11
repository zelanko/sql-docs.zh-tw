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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e0880e1746b4b65070fb28bf8d83aadec301aa4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138183"
---
# <a name="arithmetic-errors"></a>算術錯誤
ODBC 驅動程式會在提取每個資料列時，評估 SELECT 語句中的 WHERE 子句。 如果資料列包含導致算術錯誤的值（例如零除或數值溢位），驅動程式會傳回所有資料列，但會傳回具有算術錯誤之資料行的錯誤。 不過，在插入或更新時，ODBC 驅動程式會在遇到第一個算術錯誤時停止插入或更新資料。
