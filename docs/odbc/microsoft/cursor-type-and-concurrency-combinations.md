---
title: "資料指標類型和並行組合 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a20223e272ce2790a8959df3d9f7ed318e700aef
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-type-and-concurrency-combinations"></a>資料指標類型和並行的組合
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 資料指標類型來控制資料指標，提供給使用者的功能。 並行選項會控制可更新性和結果集的鎖定行為。  
  
|資料指標類型|並行存取 （允許的值）|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup>看到[使用索引鍵集驅動資料指標的限制](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)。  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK SQL_AUTOCOMMIT 連接選項設定為 SQL_AUTOCOMMIT_OFF 時，才支援。  
  
## <a name="see-also"></a>另請參閱  
 [連接選項](../../odbc/microsoft/connect-options.md)
