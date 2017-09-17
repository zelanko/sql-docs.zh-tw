---
title: "DROP TABLE 命令 |Microsoft 文件"
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
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f346bc3701df00cdddf5e6af77f500017570bd51
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="drop-table-command"></a>DROP TABLE 命令
從指定的資料來源的資料庫中移除資料表，並從磁碟中刪除。  
  
 Visual FoxPro ODBC 驅動程式支援的原生 Visual FoxPro 語言語法，此命令。 驅動程式特定資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>設定  
 *TableName*  
 指定從資料來源所指定的資料庫移除，並從磁碟刪除的資料表。  
  
 *FileName*  
 指定要刪除磁碟上的可用資料表。  
  
 ?  
 顯示您可以從中選擇資料表移除資料來源所指定的資料庫，並刪除磁碟上的 [移除] 對話方塊。  
  
## <a name="remarks"></a>備註  
 當發出卸除資料表時，所有主要的索引、 預設值，以及與資料表相關聯的驗證規則也會移除。 卸除的資料表也會影響其他資料表，如果資料表有規則指定與資料來源的資料庫或要移除的資料表相關聯的關聯性中。 規則和關聯性就不再有效時從資料庫移除資料表。  
  
## <a name="driver-remarks"></a>驅動程式註解  
 當您的應用程式傳送至資料來源的 ODBC SQL 陳述式卸除資料表時，Visual FoxPro ODBC 驅動程式會將命令轉換使用下表所示的語法，視覺化的 FoxProDROP TABLE 命令。  
  
|ODBC 語法|資料來源|Visual FoxPro 語法|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE*基底資料表名稱*|資料庫 （.dbc 檔案）|移除資料表*TableName*刪除|  
||可用的資料表 （.dbf 檔案） 的目錄|清除*dbfName*<br /><br /> 清除*cdxName*<br /><br /> 清除*fptName*|
