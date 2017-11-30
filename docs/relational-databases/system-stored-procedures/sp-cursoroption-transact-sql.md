---
title: "sp_cursoroption (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs: TSQL
helpviewer_keywords: sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0fcd7b9c009d0af70e48982f9630f783bce057d
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定資料指標選項或傳回 sp_cursoropen 預存程序所建立的資料指標資訊。 sp_cursoroption 的叫用方式指定 ID = 8，在表格式資料流 (TDS) 封包中的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>引數  
 *cursor*  
 是*處理*所產生的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 sp_cursoropen 預存程序所傳回。 *資料指標*需要**int**輸入值才能執行。  
  
 *程式碼*  
 用來保證資料指標的各種因數一定會傳回值。 *程式碼*需要下列其中一種**int**輸入值：  
  
|值|名稱|Description|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|針對某些指定的 text 或 image 資料行傳回文字指標，而不是實際的資料。<br /><br /> TEXTPTR_ONLY 可讓文字指標來作為*控點*blob 物件的更新版本可以選擇性地擷取或更新使用[!INCLUDE[tsql](../../includes/tsql-md.md)]或 DBLIB 功能 （例如：[!INCLUDE[tsql](../../includes/tsql-md.md)]READTEXT 或 DBLIB DBWRITETEXT）。<br /><br /> 如果指派 "0" 值，選取清單中的所有 text 和 image 資料行將會傳回文字指標，而不是資料。|  
|0x0002|CURSOR_NAME|在指定的名稱指派*值*至游標處。 接著，可讓 ODBC 使用[!INCLUDE[tsql](../../includes/tsql-md.md)]透過 sp_cursoropen 開啟的資料指標定位陳述式 UPDATE/DELETE。<br /><br /> 此字串可以指定為任何字元或 Unicode 資料類型。<br /><br /> 因為[!INCLUDE[tsql](../../includes/tsql-md.md)]定位陳述式 UPDATE/DELETE 運作，根據預設，在第一個資料列，在寬鬆資料指標，sp_cursor SETPOSITION 應該用來定位資料指標，然後再發出定位陳述式 UPDATE/DELETE。|  
|0x0003|TEXTDATA|在後續的提取上，針對某些 text 或 image 資料行傳回實際資料，而不是文字指標 (也就是說，這樣會復原 TEXTPTR_ONLY 的作用)。<br /><br /> 如果針對特定的資料行啟用 TEXTDATA，將會重新提取或重新整理資料列，而且可以設定回 TEXTPTR_ONLY。 如果是 TEXTPTR_ONLY，值參數是一個指定資料行編號的整數，以及傳回所有 text 或 image 資料行的零值。|  
|0x0004|SCROLLOPT|捲動選項。 如需詳細資訊，請參閱這個主題稍後的「傳回碼值」。|  
|0x0005|CCOPT|並行控制選項。 如需詳細資訊，請參閱這個主題稍後的「傳回碼值」。|  
|0x0006|ROWCOUNT|目前結果集中的資料列數目。<br /><br /> 注意： 如果正在使用非同步擴展，sp_cursoropen 所傳回的值之後可能已變更資料列計數。 如果資料列數目未知，則會傳回 –1 的值。|  
  
 *value*  
 指定所傳回的值*程式碼*。 *值*是必要的參數呼叫 0x0001、 0x0002 或 0x0003*程式碼*輸入值。  
  
> [!NOTE]  
>  A*程式碼*值為 2 表示字串資料類型。 任何其他*程式碼*輸入或傳回值*值*是整數。  
  
## <a name="return-code-values"></a>傳回碼值  
 *值*參數可能會傳回下列其中一種*程式碼*值。  
  
|傳回值|Description|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *值*參數會傳回下列 SCROLLOPT 值之一。  
  
|傳回值|Description|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *值*參數會傳回下列 CCOPT 值之一。  
  
|傳回值|Description|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 或 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
