---
title: 資料庫引擎設定-Filestream |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], about FILESTREAM
ms.assetid: 641a10a1-ae52-4d26-8f1c-a032a4aeff02
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ab12b507246a3e13ac59be213813604d531d9a28
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012727"
---
# <a name="database-engine-configuration---filestream"></a>Database Engine 組態 - Filestream
  您可以使用這個頁面，針對這個 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝啟用 FILESTREAM。 FILESTREAM 會將 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 與 NTFS 檔案系統整合，方法是 `varbinary(max)` 將二進位大型物件（BLOB）資料儲存為檔案系統上的檔案。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可以插入、更新、查詢、搜尋和備份 FILESTREAM 資料。 Win32 檔案系統介面提供了資料的資料流方式存取。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **對 Transact-SQL 存取啟用 FILESTREAM**  
 選取此選項即可針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取啟用 FILESTREAM。 您必須先核取這個控制項，然後才能使用其他控制選項。  
  
 **對檔案 I/O 資料流存取啟用 FILESTREAM**  
 選取此選項即可針對 Win32 資料流存取啟用 FILESTREAM。  
  
 **Windows 共用名稱**  
 使用這個控制項即可輸入即將儲存 FILESTREAM 資料之 Windows 共用的名稱。  
  
 **允許遠端用戶端具有 FILESTREAM 資料的資料流存取權**  
 選取這個控制項即可允許遠端用戶端在此伺服器上存取這項 FILESTREAM 資料。  
  
## <a name="see-also"></a>另請參閱  
 [啟用和設定 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
