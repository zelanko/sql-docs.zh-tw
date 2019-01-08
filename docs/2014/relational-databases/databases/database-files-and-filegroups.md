---
title: 資料庫檔案與檔案群組 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d75dee637a5579ca3f189e14333fbf9356623d0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790110"
---
# <a name="database-files-and-filegroups"></a>資料庫檔案與檔案群組
  基本上，每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫都有兩個作業系統檔案：資料檔與記錄檔。 資料檔包含諸如資料表、索引、預存程序以及檢視等資料和物件。 記錄檔包含復原資料庫中所有交易必要的資訊。 資料檔可以組成檔案群組，以方便配置及管理。  
  
## <a name="database-files"></a>資料庫檔案  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有三種檔案類型，如下表所示。  
  
|檔案|描述|  
|----------|-----------------|  
|主要|主要資料檔包含資料庫啟動資訊，並指到資料庫中的其他檔案。 使用者資料和物件可儲存於此檔案或次要的資料檔中。 每個資料庫都有一個主要資料檔案。 建議您將主要資料檔的副檔名設為 .mdf。|  
|次要|次要資料檔是選擇性且使用者自訂的，並可儲存使用者資料。 次要檔可用以將資料分散在多個磁碟上，即透過將每個檔案放在不同的磁碟機上來達成此目的。 此外，若資料庫超過了單一 Windows 檔案的大小上限，您可使用次要資料檔，以容許資料庫繼續成長。<br /><br /> 建議您將次要資料檔的副檔名設為 .ndf。|  
|交易記錄|交易記錄檔包含了用來復原資料庫的記錄資訊。 每個資料庫至少要有一個記錄檔。 建議的交易記錄檔的副檔名為 .ldf。|  
  
 例如，一個簡單的資料庫 **Sales** 可由一個包含所有資料和物件的主要檔案，以及一個包含交易記錄資訊的記錄檔所組成。 也可以建立名稱為 **Orders** 的複雜資料庫，以包含一個主要檔案和五個次要檔案。 在資料庫中的資料和物件平均分散於總共六個檔案中，而且有四個記錄檔包含交易記錄資訊。  
  
 依預設，資料和交易記錄會放置在相同的磁碟和路徑中。 這是透過處理單一磁碟系統來完成。 然而，這對於實際執行環境可能不是最合適的。 我們建議您將資料和記錄檔放在不同的磁碟上。  
  
## <a name="filegroups"></a>檔案群組  
 每個資料庫有一個主要的檔案群組。 此檔案群組可能包含主要資料檔和未放入其他檔案群組的次要檔案。 可建立使用者自訂檔案群組來將資料檔群組在一起，以利管理、資料配置和放置之用。  
  
 例如，您以可將三個檔案 (Data1.ndf、Data2.ndf 以及 Data3.ndf) 分別建立於三台磁碟機內，並將它們指派至檔案群組 **fgroup1**。 接著您可根據檔案群組 **fgroup1**來建立資料表。 資料表的資料查詢可分散至三個磁碟，藉此改善效能。 另一個改善效能的作法是將單一檔案建立在 RAID (獨立磁碟的重複陣列，通稱磁碟陣列) 的條狀磁碟組上。 然而，檔案和檔案群組都可讓您輕鬆地將新的檔案加至新的磁碟內。  
  
 所有儲存在檔案群組中的資料檔列於下表。  
  
|檔案群組|描述|  
|---------------|-----------------|  
|主要|包含主要檔案的檔案群組。 所有的系統資料表都配置於主要檔案群組內。|  
|使用者自訂|使用者在初次建立資料庫或之後修改資料庫時，特別建立的檔案群組。|  
  
### <a name="default-filegroup"></a>預設的檔案群組  
 若在資料庫中建立物件時未指明屬於哪個檔案群組，就會將物件指定至預設的檔案群組。 在任何時候，都只有一個檔案群組指定為預設檔案群組。 在預設檔案群組中的檔案必須夠大，才能容納未配置到其他檔案群組的新物件。  
  
 除非使用 ALTER DATABASE 陳述式加以變更，否則 PRIMARY 檔案群組就是預設的檔案群組。 系統物件和資料表仍配置於 PRIMARY 檔案群組內，而非新的預設檔案群組之中。  
  
## <a name="related-content"></a>相關內容  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
 [資料庫卸離和附加 &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
