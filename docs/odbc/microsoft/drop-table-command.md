---
title: DROP TABLE 指令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 779c519f720027aea3a6f6cf2587d3c6e0b59b52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303419"
---
# <a name="drop-table-command"></a>DROP TABLE 命令
從使用數據源指定的資料庫中刪除表,並將其從磁盤中刪除。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的本機 Visual FoxPro 語言文法。 有關特定於驅動程序的資訊,請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>設定  
 *表格名稱*  
 指定要從使用數據源指定的資料庫中刪除的表,並從磁盤中刪除表。  
  
 *檔案名稱*  
 指定要從磁碟中刪除的可用表。  
  
 ?  
 顯示"刪除"對話框,您可以從中選擇一個表,以便從使用數據源指定的資料庫中刪除,並從磁盤中刪除。  
  
## <a name="remarks"></a>備註  
 發出 DROP TABLE 時,還將刪除與表關聯的所有主索引、預設值和驗證規則。 如果資料庫具有與要刪除的表關聯的規則或關係,則 DROP TABLE 還會影響資料庫中用數據來源指定的其他表。 當從資料庫中刪除表時,規則和關係不再有效。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當應用程式將 ODBC SQL 語句 DROP TABLE 傳送到資料來源時,Visual FoxPro ODBC 驅動程式使用下表中顯示的語法將該命令轉換為 Visual FoxProDROP TABLE 命令。  
  
|ODBC 語法|資料來源|視覺化 FoxPro 語法|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE*基表名稱*|資料庫(.dbc 檔案)|移除*表格名稱*移除|  
||可用表格(.dbf 檔案)|ERASE *dbf 名稱*<br /><br /> ERASE *cdx 名稱*<br /><br /> ERASE *fpt 名稱*|
