---
title: sp_cursoroption （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: stevestein
ms.author: sstein
ms.openlocfilehash: dce66e74f7415a8ff5ac6de4505d8a1f0632391b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108450"
---
# <a name="sp_cursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定資料指標選項，或傳回由 sp_cursoropen 預存程式所建立的資料指標資訊。 sp_cursoroption 的叫用方式是在表格式資料流程（TDS）封包中指定 ID = 8。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>引數  
 *cursor*  
 這是由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所產生並由 sp_cursoropen 預存程式所傳回的*控制碼*值。 資料*指標*需要**int**輸入值才能執行。  
  
 *錯誤碼*  
 用來保證資料指標的各種因數一定會傳回值。 程式*代碼*需要下列其中一個**int**輸入值：  
  
|值|名稱|描述|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|針對某些指定的 text 或 image 資料行傳回文字指標，而不是實際的資料。<br /><br /> TEXTPTR_ONLY 允許使用文字指標做為 blob 物件的*控制碼*，稍後可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]或 DBLIB 設施（例如[!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT 或 DBLIB DBWRITETEXT）選擇性地抓取或更新它們。<br /><br /> 如果指派 "0" 值，選取清單中的所有 text 和 image 資料行將會傳回文字指標，而不是資料。|  
|0x0002|CURSOR_NAME|將 [*值*] 中指定的名稱指派給資料指標。 接著，這可讓 ODBC 在透過 sp_cursoropen [!INCLUDE[tsql](../../includes/tsql-md.md)]開啟的資料指標上使用定位 UPDATE/DELETE 子句。<br /><br /> 此字串可以指定為任何字元或 Unicode 資料類型。<br /><br /> 由於[!INCLUDE[tsql](../../includes/tsql-md.md)]定位的 UPDATE/delete 語句預設會在 fat 資料指標的第一個資料列上運作，因此在發出定位的 UPDATE/delete 語句之前，應該先使用 sp_cursor SETPOSITION 來定位資料指標。|  
|0x0003|TEXTDATA|在後續的提取上，針對某些 text 或 image 資料行傳回實際資料，而不是文字指標 (也就是說，這樣會復原 TEXTPTR_ONLY 的作用)。<br /><br /> 如果針對特定的資料行啟用 TEXTDATA，將會重新提取或重新整理資料列，而且可以設定回 TEXTPTR_ONLY。 如果是 TEXTPTR_ONLY，值參數是一個指定資料行編號的整數，以及傳回所有 text 或 image 資料行的零值。|  
|0x0004|SCROLLOPT|捲動選項。 如需詳細資訊，請參閱這個主題稍後的「傳回碼值」。|  
|0x0005|CCOPT|並行控制選項。 如需詳細資訊，請參閱這個主題稍後的「傳回碼值」。|  
|0x0006|ROWCOUNT|目前結果集中的資料列數目。<br /><br /> 注意：如果正在使用非同步擴展，資料列計數可能會因為 sp_cursoropen 傳回的值而變更。 如果未知的資料列數目，則會傳回值-1。|  
  
 *value*  
 指定程式*代碼*所傳回的值。 *value*是必要的參數，它會呼叫0x0001、0x0002 或0x0003 程式*代碼*輸入值。  
  
> [!NOTE]  
>  2的*代碼*值為字串資料類型。 任何其他以傳*值*方式輸入或傳回的程式*代碼*值都是整數。  
  
## <a name="return-code-values"></a>傳回碼值  
 *Value*參數可能會傳回下列其中一個程式*代碼*值。  
  
|傳回值|描述|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *Value*參數會傳回下列其中一個 SCROLLOPT 值。  
  
|傳回值|描述|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *Value*參數會傳回下列其中一個 CCOPT 值。  
  
|傳回值|描述|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 或 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
