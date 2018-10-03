---
title: DROP TABLE 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0865502928e98329764ae6085ab2b67aa26f0517
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47852296"
---
# <a name="drop-table-command"></a>DROP TABLE 命令
移除與資料來源所指定的資料庫中的資料表，並從磁碟中予以刪除。  
  
 Visual FoxPro ODBC Driver 支援原生 Visual FoxPro 語言語法，此命令。 驅動程式專屬資訊，請參閱 < 備註 >。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>[設定]  
 *TableName*  
 指定的資料表來移除與資料來源所指定的資料庫，並從磁碟刪除。  
  
 *FileName*  
 指定可用的資料表，以從磁碟刪除。  
  
 ?  
 顯示 [移除] 對話方塊，您可以從中選擇移除與資料來源所指定的資料庫，並從磁碟刪除的資料表。  
  
## <a name="remarks"></a>備註  
 當發出卸除資料表時，所有主要的索引，預設值，以及與資料表相關聯的驗證規則也會移除。 卸除資料表也會影響其他資料表中要移除的資料表相關聯的關聯性的資料庫指定與資料來源，如果資料表有規則。 規則和關聯性已不再有效時從資料庫移除資料表。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式傳送至資料來源的 ODBC SQL 陳述式卸除資料表時，則 Visual FoxPro ODBC Driver 會將命令轉換 Visual FoxProDROP 資料表命令，使用下表所示的語法。  
  
|ODBC 語法|資料來源|Visual FoxPro 語法|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE*基底資料表名稱*|資料庫 （.dbc 檔案）|移除資料表*TableName*刪除|  
||可用的資料表 （.dbf 檔案） 的目錄|清除*dbfName*<br /><br /> 清除*cdxName*<br /><br /> 清除*fptName*|
