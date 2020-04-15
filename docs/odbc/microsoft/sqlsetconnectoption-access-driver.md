---
title: SQLSetConnectOption(存取驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e5f15575d34031d9886219af5677b4fc5f1d5aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301531"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Access 驅動程式)
> [!NOTE]  
>  本主題提供特定於訪問驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|fOption|註解|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以設置為SQL_MODE_READ_ONLY或SQL_MODE_READ_WRITE。 但是,如果SQL_ACCESS_MODE設置為SQL_MODE_READ_ONLY,則驅動程式不會阻止更新。|  
|SQL_AUTOCOMMIT|使用 Microsoft Access 驅動程式時,SQL_AUTOCOMMIT 選項可以設置為SQL_AUTOCOMMIT_ON或SQL_AUTOCOMMIT_OFF,因為 Microsoft Access 驅動程式支援事務[1]。|  
|SQL_CURRENT_QUALIFIER|支援。|  
|SQL_LOGIN_TIMEOUT|不支援。|  
|SQL_OPT_TRACE|支援。|  
|SQL_OPT_TRACEFILE|支援。|  
|SQL_PACKET_SIZE|不支援。|  
|SQL_QUIET_MODE|不支援。|  
|SQL_TRANSLATE_DLL|不支援。|  
|SQL_TRANSLATION_OPTION|不支援。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION總是SQL_TXN_READ_COMMITTED。|  
  
 [1] 微軟存取驅動程式不支援原子事務。 使用 Microsoft Access 驅動程式提交事務時,提交事務的時間與將值寫入磁碟之間的延遲有限。 此延遲由 Microsoft Jet 引擎固有的延遲決定。 即使"PageTimeout"選項設置為低於該值,頁面超時也不會小於最小值。 因此,無法保證提交的數據是穩定的,因為可能在延遲期間進行更改。
