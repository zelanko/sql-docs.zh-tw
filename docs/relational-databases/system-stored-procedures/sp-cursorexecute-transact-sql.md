---
title: sp_cursorexecute (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cc46446c64fe247eee88ae08628032793cbebb2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spcursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  根據 sp_cursorprepare 所建立的執行計畫來建立及擴展資料指標。 此程序，結合 sp_cursorprepare，具有相同的函數 sp_cursoropen，但是會分成兩個階段。 sp_cursorexecute 的叫用方式指定 ID = 4 在表格式資料流 (TDS) 封包中的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>引數  
 *prepared_handle*  
 已備妥的陳述式*處理*sp_cursorprepare 所傳回的值。 *prepared_handle*是必要的參數呼叫**int**輸入值。  
  
 *cursor*  
 這是 SQL Server 產生的資料指標識別碼。 *資料指標*游標處，例如 sp_cursorfetch 處理的所有後續程序上都必須提供必要參數  
  
 *scrollopt*  
 捲動選項。 *scrollopt*是選擇性的參數需要**int**輸入值。 Sp_cursorexecute*scrollopt*參數具有相同的值選項與 sp_cursoropen 的。  
  
> [!NOTE]  
>  不支援 PARAMETERIZED_STMT 值。  
  
> [!IMPORTANT]  
>  如果*scrollopt*未指定值，預設值為 KEYSET，不論*scrollopt* sp_cursorprepare 中指定的值。  
  
 *ccopt*  
 貨幣控制選項。 *ccopt*是選擇性的參數需要**int**輸入值。 Sp_cursorexecute*ccopt*參數具有相同的值選項與 sp_cursoropen 的。  
  
> [!IMPORTANT]  
>  如果*ccopt*未指定值，預設值為 OPTIMISTIC，不論*ccopt* sp_cursorprepare 中指定的值。  
  
 *資料列計數*  
 這是選擇性參數，表示要搭配 AUTO_FETCH 使用的提取緩衝區資料列數目。 預設為 20 個資料列。 *資料列計數*當指派為輸入值與傳回值時，表現。  
  
|當做輸入值|當做傳回值|  
|--------------------|---------------------|  
|當指定 AUTO_FETCH 與 FAST_FORWARD 資料指標*rowcount*代表要放入提取緩衝區資料列數目。|代表結果集中的資料列數目。 當*scrollopt*指定 AUTO_FETCH 值時， *rowcount*傳回提取到提取緩衝區的資料列數目。|  
  
 *bound_param*  
 指定選擇性使用其他參數。  
  
> [!NOTE]  
>  第五個之後的任何參數都會當做輸入參數傳遞給陳述式計畫。  
  
## <a name="code-return-value"></a>程式碼傳回值  
 *資料列計數*可能會傳回下列值。  
  
|Value|Description|  
|-----------|-----------------|  
|-1|未知的資料列數目。|  
|-n|非同步擴展在作用中。|  
  
## <a name="remarks"></a>備註  
  
## <a name="scrollopt-and-ccopt-parameters"></a>scrollopt 和 ccopt 參數  
 *scrollopt*和*ccopt*快取的計畫被佔用伺服器快取，這表示必須重新編譯識別陳述式的已備妥控制代碼時很有用。 *Scrollopt*和*ccopt*參數值必須符合在 sp_cursorprepare 的原始要求中傳送的值。  
  
> [!NOTE]  
>  PARAMETERIZED_STMT 不應該指派給*scrollopt*。  
  
 當無法提供相符的值時將會導致重新編譯計劃，取消準備和執行作業。  
  
## <a name="rpc-and-tds-considerations"></a>RPC 和 TDS 考量  
 RPC RETURN_METADATA 輸入旗標可以設定為 1，要求在 TDS 資料流中傳回資料指標選取清單中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursoropen &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
