---
title: "FileTable 結構描述 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 78856216342e00ee4af547d8c39d132c57eac575
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="filetable-schema"></a>FileTable 結構描述
  描述 FileTable 預先定義且固定的結構描述。  
  
|檔案屬性名稱|型別|大小|預設值|描述|檔案系統可存取性|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|**hierarchyid**|變數|識別此項目位置的 **hierarchyid** 。|此節點在階層式 FileNamespace 中的位置。<br /><br /> 資料表的主索引鍵。|可透過設定 Windows 路徑值加以建立及修改。|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||**NEWID()** 函數所傳回的值。|FILESTREAM 資料的唯一識別碼。|不適用。|  
|**file_stream**|**varbinary(max)**<br /><br /> **檔案資料流**|變數|NULL|包含 FILESTREAM 資料。|不適用。|  
|**file_type**|**nvarchar(255)**|變數|NULL。<br /><br /> 檔案系統中的建立或重新命名作業，將會根據名稱填入副檔名值。|代表檔案的類型。<br /><br /> 當您建立全文檢索索引時，此資料行可用以作為 **TYPE COLUMN** 。<br /><br /> **file_type** 是保存的計算資料行。|自動計算， 無法設定。|  
|**名稱**|**nvarchar(255)**|變數|GUID 值。|檔案或目錄名稱。|可使用 Windows API 加以建立或修改。|  
|**parent_path_locator**|**hierarchyid**|變數|**hierarchyid** ，識別內含此項目的目錄。|上層目錄的 **hierarchyid** 。<br /><br /> **parent_path_locator** 是保存的計算資料行。|自動計算， 無法設定。|  
|**cached_file_size**|**bigint**|||FILESTREAM 資料的大小 (以位元組為單位)。<br /><br /> **cached_file_size** 是保存的計算資料行。|雖然快取的檔案大小會自動保持最新狀態，不過在少見的情況下，它可能會呈現未同步狀態。 若要計算確切的大小，請使用 **DATALENGTH()** 函數。|  
|**creation_time**|**datetime2(4)**<br /><br /> **非 Null**|8 個位元組|目前時間。|建立檔案的日期與時間。|自動計算， 也可以使用 Windows API 加以設定。|  
|**last_write_time**|**datetime2(4)**<br /><br /> **非 Null**|8 個位元組|目前時間。|上次更新檔案的日期與時間。|自動計算， 也可以使用 Windows API 加以設定。|  
|**last_access_time**|**datetime2(4)**<br /><br /> **非 Null**|8 個位元組|目前時間。|上次存取檔案的日期與時間。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_directory**|**bit**<br /><br /> **非 Null**|1 個位元組|FALSE|指出資料列是否代表目錄。 此值會自動計算，而且無法設定。|自動計算， 無法設定。|  
|**is_offline**|**bit**<br /><br /> **非 Null**|1 個位元組|FALSE|離線檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_hidden**|**bit**<br /><br /> **非 Null**|1 個位元組|FALSE|隱藏檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_readonly**|**bit**<br /><br /> **非 Null**|1 個位元組|FALSE|唯讀檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_archive**|**bit**<br /><br /> **非 Null**|1 個位元組|FALSE|封存屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_system**|**bit**<br /><br /> **非 Null**|1 個位元組|FALSE|系統檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
|**is_temporary**|**bit**<br /><br /> **非 Null**|1 個位元組|FALSE|暫存檔案屬性。|自動計算， 也可以使用 Windows API 加以設定。|  
  
## <a name="see-also"></a>另請參閱  
 [建立、改變及卸除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
  
  
