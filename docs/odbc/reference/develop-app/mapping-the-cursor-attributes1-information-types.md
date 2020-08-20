---
description: 對應資料指標 Attributes1 資訊類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcd4c1eaa6ddd2e6db4f2634cc22d3148e7977cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461400"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>對應資料指標 Attributes1 資訊類型
當 ODBC 3。*x* 應用程式會呼叫 odbc 2.x 驅動程式中的 **SQLGetInfo** ，其中包含動態、順向、索引鍵集*驅動程式或* 靜態資料指標) 所 (的 SQL_XXXX_CURSOR_ATTRIBUTES1 資訊類型，驅動程式管理員所傳回的位的設定取決於 ODBC 2。*x* 驅動程式會針對對應的 ODBC 2 傳回。*x* 資訊類型。 這些位設定如下表所示。  
  
|位在<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|資料指標類型|ODBC 2。*x* 資訊<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|全部|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|動態、索引鍵集驅動程式、靜態|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|動態、索引鍵集驅動程式、靜態|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|全部|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|動態、索引鍵集驅動程式、靜態|SQL_POS_OPERATIONS|
