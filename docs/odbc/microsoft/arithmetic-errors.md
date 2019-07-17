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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138183"
---
# <a name="arithmetic-errors"></a>算術錯誤
ODBC 驅動程式會評估中的 SELECT 陳述式的 WHERE 子句，因為它會擷取每個資料列。 如果資料列都包含值，會導致算術錯誤，例如除以零或數字溢位，這個值會傳回所有資料列，驅動程式，但會傳回錯誤資料行發生算術錯誤。 當插入或更新，不過，ODBC 驅動程式會停止插入或更新資料，在遇到第一個的算術錯誤時。
