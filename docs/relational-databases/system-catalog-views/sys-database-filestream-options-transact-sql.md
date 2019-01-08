---
title: sys.database_filestream_options & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_filestream_options
- sys.database_filestream_options_TSQL
- database_filestream_options_TSQL
- sys.database_filestream_options
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_filestream_options catalog view
ms.assetid: 3383c607-0bbc-456a-ab37-7230f4cbf0e9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3038b27084dce6a84436e658c66b77dc61ead49e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543016"
---
# <a name="sysdatabasefilestreamoptions-transact-sql"></a>sys.database_filestream_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示 FileTable 中已啟用的非交易式 FILESTREAM 資料存取層級的相關資訊。 針對 SQL Server 執行個體中的每個資料庫，各包含一個資料列。  
  
 如需有關 FileTable 的詳細資訊，請參閱 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)。  
  
  
|「資料行」|類型|描述|  
|------------|----------|-----------------|  
|**database_id**|**int**|資料庫的識別碼。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內，這個值是唯一的。|  
|**directory_name**|**nvarchar(255)**|所有 FileTable 命名空間的資料庫層級目錄。|  
|**non_transacted_access**|**tinyint**|已啟用的非交易式 FILESTREAM 資料存取層級。 存取層級選項所設定 NON_TRANSACTED_ACCESS **CREATE DATABASE**或是**ALTER DATABASE**陳述式。<br /><br /> 這個設定有下列其中一個值：<br /><br /> 0-未啟用。 這是預設值。 所提供的值設定這個層級**OFF** for **NON_TRANSACTED_ACCESS**選項。<br /><br /> 1-唯讀存取權。 所提供的值設定這個層級**READ_ONLY** for **NON_TRANSACTED_ACCESS**選項。<br /><br /> 3-完整的存取權。 所提供的值設定這個層級**完整**for **NON_TRANSACTED_ACCESS**選項。<br /><br /> 5 - 正在轉換為 READONLY<br /><br /> 6-正在轉換為 OFF|  
|**non_transacted_access_desc**|**nvarchar(60)**|Non_transacted_access 中識別的非交易式存取層級的描述。<br /><br /> 這個設定有下列其中一個值：<br /><br /> NONE-這是預設值。<br /><br /> READ_ONLY<br /><br /> FULL<br /><br /> IN_TRANSITION_TO_READ_ONLY<br /><br /> IN_TRANSITION_TO_OFF|  
  
## <a name="see-also"></a>另請參閱  
 [啟用 FileTable 的必要條件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
  
