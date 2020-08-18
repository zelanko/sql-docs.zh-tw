---
description: DROP TABLE 命令
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f383740584ca524c732172ee363f7ffb393c30c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412564"
---
# <a name="drop-table-command"></a>DROP TABLE 命令
從指定的資料庫中移除具有資料來源的資料表，並將它從磁片中刪除。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的原生 Visual FoxPro 語言語法。 如需驅動程式特定的資訊，請參閱備註。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>設定  
 *名*  
 指定要從資料來源指定的資料庫中移除的資料表，並從磁片中刪除。  
  
 *FileName*  
 指定要從磁片刪除的免費資料表。  
  
 ?  
 顯示 [移除] 對話方塊，您可以從這個對話方塊選擇要從資料來源指定的資料庫中移除的資料表，以及從磁片刪除的資料表。  
  
## <a name="remarks"></a>備註  
 發出 DROP TABLE 時，也會一併移除所有的主要索引、預設值，以及與資料表相關聯的驗證規則。 如果這些資料表具有與要移除之資料表相關聯的規則或關聯，則 DROP TABLE 也會影響資料庫中以資料來源指定的其他資料表。 從資料庫中移除資料表時，規則和關聯不再有效。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句放置資料表傳送到資料來源時，Visual FoxPro ODBC 驅動程式會使用下表所示的語法，將命令轉換成 Visual FoxProDROP TABLE 命令。  
  
|ODBC 語法|資料來源|Visual FoxPro 語法|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE *-資料表名稱*|資料庫 ( dbc 檔案) |移除資料表 *TableName* 刪除|  
||任意資料表 ( .dbf 檔的目錄) |清除 *dbfName*<br /><br /> 清除 *cdxName*<br /><br /> 清除 *fptName*|
