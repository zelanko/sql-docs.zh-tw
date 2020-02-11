---
title: 對應資料指標 Attributes1 資訊類型 |Microsoft Docs
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
ms.openlocfilehash: d95d3e67fdcd7159074e2f20ffa558f4c80bbcb2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036348"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>對應資料指標 Attributes1 資訊類型
當 ODBC 3 時。*x*應用程式會使用 SQL_XXXX_CURSOR_ATTRIBUTES1 資訊類型（適用于動態、順向、索引鍵集驅動程式或靜態資料指標）來呼叫 odbc 2.x 驅動程式中的**SQLGetInfo** ，而驅動程式管理員所傳回的位設定則取決於*ODBC 2。**x*驅動程式會傳回對應 ODBC 2 的。*x*資訊類型。 位的設定如下表所示。  
  
|中的位<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|資料指標類型|ODBC 2。*x*資訊<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|全部|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|動態、索引鍵集驅動程式、靜態|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|動態、索引鍵集驅動程式、靜態|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|全部|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|動態、索引鍵集驅動程式、靜態|SQL_POS_OPERATIONS|
