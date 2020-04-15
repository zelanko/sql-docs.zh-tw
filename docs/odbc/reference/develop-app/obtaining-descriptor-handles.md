---
title: 取得描述符句柄 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c17b693080c2727d2ee788b74f247d86d7a3cb27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302343"
---
# <a name="obtaining-descriptor-handles"></a>取得描述項控制代碼
應用程序獲取任何顯式分配的描述符的句柄,作為對**SQLAllocHandle**的調用的輸出參數。 隱式分配的描述符的句柄是通過調用**SQLGetStmtAttr**獲得的。
