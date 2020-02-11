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
ms.openlocfilehash: 278950bac7589b8a6b02d894c8133a699c3bd1ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071799"
---
# <a name="drop-table-command"></a>DROP TABLE 命令
從以資料來源指定的資料庫中移除資料表，並將它從磁片中刪除。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的原生 Visual FoxPro 語言語法。 如需驅動程式特定的資訊，請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>設定  
 *TableName*  
 指定要從使用資料來源所指定的資料庫中移除的資料表，並從磁片中刪除。  
  
 *名稱*  
 指定要從磁片刪除的免費資料表。  
  
 ?  
 顯示 [移除] 對話方塊，您可以從中選擇要從使用資料來源所指定的資料庫中移除的資料表，並從磁片刪除。  
  
## <a name="remarks"></a>備註  
 當發出 DROP TABLE 時，也會一併移除與資料表相關聯的所有主要索引、預設值和驗證規則。 DROP TABLE 也會影響資料庫中使用資料來源所指定的其他資料表（如果這些資料表具有與要移除之資料表相關聯的規則或關聯）。 當資料表從資料庫中移除時，規則和關聯不再有效。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句卸載資料表傳送到資料來源時，Visual FoxPro ODBC 驅動程式會使用下表所示的語法，將命令轉換成 Visual FoxProDROP TABLE 命令。  
  
|ODBC 語法|資料來源|Visual FoxPro 語法|  
|-----------------|-----------------|--------------------------|  
|卸載資料表*基底-資料表名稱*|資料庫（. dbc 檔案）|移除資料表*TableName*刪除|  
||可用的資料表目錄（.dbf 檔案）|清除*dbfName*<br /><br /> 清除*cdxName*<br /><br /> 清除*fptName*|
