---
title: 算術錯誤 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299898"
---
# <a name="arithmetic-errors"></a>算術錯誤
ODBC 驅動程式在獲取每行時評估 SELECT 語句中的 WHERE 子句。 如果行包含導致算術錯誤的值(如除以零或數位溢出),則驅動程式將返回所有行,但返回具有算術錯誤的列的錯誤。 但是,當插入或更新時,當遇到第一個算術錯誤時,ODBC 驅動程式將停止插入或更新數據。
