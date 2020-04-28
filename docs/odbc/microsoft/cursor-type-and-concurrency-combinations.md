---
title: 資料指標類型和並行組合 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6397b5d675546bf41102f037b68c0022bec74df
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280768"
---
# <a name="cursor-type-and-concurrency-combinations"></a>資料指標類型和並行組合
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 資料指標類型可控制提供給使用者的資料指標功能。 並行選項控制結果集的更新性和鎖定行為。  
  
|資料指標類型|並行（允許的值）|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup>請參閱[使用索引鍵集驅動資料指標的限制](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)。  
  
 <sup>[2]</sup>只有在 SQL_AUTOCOMMIT 連接選項設定為 [SQL_AUTOCOMMIT_OFF] 時，才支援 SQL_CONCUR_LOCK。  
  
## <a name="see-also"></a>另請參閱  
 [連接選項](../../odbc/microsoft/connect-options.md)
