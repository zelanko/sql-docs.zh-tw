---
title: 將資料指標 Attributes1 資訊類型對應 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e9549c442e301f3a6ed8d3da9c73d52177adf01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628891"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>對應資料指標 Attributes1 資訊類型
當 ODBC 3。*x*應用程式會呼叫**SQLGetInfo** ODBC 2 *.x* SQL_XXXX_CURSOR_ATTRIBUTES1 資訊類型的驅動程式 (如動態、 順向的索引鍵集驅動程式，或靜態資料指標），傳回由驅動程式管理員的位元設定會取決於何種 ODBC 2。*x*驅動程式會傳回對應的 ODBC 2。*x*資訊類型。 位元會設定下表所示。  
  
|位元<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|資料指標類型|ODBC 2。*x*資訊<br /><br /> 型別|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|動態的索引鍵集驅動程式靜態|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|動態的索引鍵集驅動程式靜態|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|動態的索引鍵集驅動程式靜態|SQL_POS_OPERATIONS|
