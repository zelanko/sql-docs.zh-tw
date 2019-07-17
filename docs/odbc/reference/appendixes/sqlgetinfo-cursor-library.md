---
title: SQLGetInfo （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Cursor Library
ms.assetid: 1b4d220d-2c07-4f56-987e-36813bb1a6ce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f115ded8392ddc3dcac32c2477794c007d5eb81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073919"
---
# <a name="sqlgetinfo-cursor-library"></a>SQLGetInfo (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLGetInfo**資料指標程式庫中的函式。 如需一般資訊**SQLGetInfo**，請參閱[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 資料指標程式庫會傳回下列值的值*資訊類型*(&#124;代表位元 OR); 對於所有其他的值*資訊類型*，它會呼叫**SQLGetInfo**在 驅動程式。  
  
|*InfoType*|傳回值|  
|----------------|--------------------|  
|SQL_BOOKMARK_PERSISTENCE|SQL_BP_SCROLL|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|0|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|0|  
|SQL_FETCH_DIRECTION[1]|SQL_FD_FETCH_ABSOLUTE &#124; SQL_FD_FETCH_FIRST &#124; SQL_FD_FETCH_LAST &#124; SQL_FD_FETCH_NEXT &#124; SQL_FD_FETCH_PRIOR &#124; SQL_FD_FETCH_RELATIVE &#124; SQL_FD_FETCH_BOOKMARK|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124; SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_CONCURRENCY &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_GETDATA_EXTENSIONS|SQL_GD_BLOCK&#124;任何驅動程式所傳回的值**附註：** 當資料擷取**SQLFetchScroll**， **SQLGetData**支援 SQL_GD_ANY_COLUMN 和 SQL_GD_BOUND 位元遮罩所指定的功能。|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES1|0|  
|SQL_KEYSET_DRIVEN_CURSOR_ATTRIBUTES2|0|  
|SQL_LOCK_TYPES[1]|SQL_LCK_NO_CHANGE|  
|SQL_STATIC_CURSOR_ATTRIBUTES1|SQL_CA1_NEXT &#124; SQL_CA1_ABSOLUTE &#124; SQL_CA1_RELATIVE &#124; SQL_CA1_BOOKMARK &#124; SQL_CA1_LOCK_NO_CHANGE &#124; SQL_CA1_POS_POSITION &#124; SQL_CA1_POSITIONED_DELETE &#124; SQL_CA1_POSITIONED_UPDATE &#124;SQL_CA1_SELECT_FOR_UPDATE|  
|SQL_STATIC_CURSOR_ATTRIBUTES2|SQL_CA2_READ_ONLY_CONCUR &#124; SQL_CA2_OPT_VALUES_ CONCURRENCY &#124; SQL_CA2_SENSITIVITY_UPDATES|  
|SQL_POS_OPERATIONS[1]|SQL_POS_POSITION|  
|SQL_POSITIONED_STATEMENTS[1]|SQL_PS_POSITIONED_DELETE &#124; SQL_PS_POSITIONED_UPDATE &#124; SQL_PS_SELECT_FOR_UPDATE|  
|SQL_ROW_UPDATES|"Y"|  
|SQL_SCROLL_CONCURRENCY[1]|SQL_SCCO_READ_ONLY &#124; SQL_SCCO_OPT_VALUES|  
|SQL_SCROLL_OPTIONS|SQL_SO_FORWARD_ONLY &#124; SQL_SO_STATIC|  
|SQL_STATIC_SENSITIVITY[1]|SQL_SS_UPDATES|  
  
 [1] 只有在資料指標程式庫搭配 ODBC 2.x 驅動程式時，才使用。  
  
> [!IMPORTANT]  
>  當交易認可或回復為資料來源時，資料指標程式庫會實作相同的資料指標行為。 也就是說，認可或回復交易，藉由呼叫**SQLEndTran**或藉由使用 SQL_ATTR_AUTOCOMMIT 連接屬性，可能會導致要刪除的存取方案，然後關閉所有陳述式的資料指標的資料來源在連線上。 如需詳細資訊，請參閱 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊中的和類型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。
