---
description: sp_cursorexecute (Transact-SQL)
title: sp_cursorexecute (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07795588a4c1d6df43a7041f9254a661e527be14
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543582"
---
# <a name="sp_cursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  根據 sp_cursorprepare 所建立的執行計畫來建立及擴展資料指標。 此程式與 sp_cursorprepare 結合，與 sp_cursoropen 具有相同的功能，但會分割成兩個階段。 sp_cursorexecute 的叫用方式是在表格式資料流程 (TDS) 封包中指定 ID = 4。  
  
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
 這是 sp_cursorprepare 所傳回的備妥語句 *控制碼* 值。 *prepared_handle* 是呼叫 **int** 輸入值的必要參數。  
  
 *cursor*  
 這是 SQL Server 產生的資料指標識別碼。 *cursor* 是必要的參數，在所有處理資料指標的後續程式上都必須提供此參數，例如 sp_cursorfetch  
  
 *scrollopt*  
 捲動選項。 *scrollopt* 是需要 **int** 輸入值的選擇性參數。 Sp_cursorexecute*scrollopt* 參數的值選項與 sp_cursoropen 的參數相同。  
  
> [!NOTE]  
>  不支援 PARAMETERIZED_STMT 值。  
  
> [!IMPORTANT]  
>  如果未指定 *scrollopt* 值，則不論 sp_cursorprepare 中指定的 *scrollopt* 值為何，預設值都是索引鍵集。  
  
 *ccopt*  
 貨幣控制選項。 *ccopt* 是需要 **int** 輸入值的選擇性參數。 Sp_cursorexecute*ccopt* 參數的值選項與 sp_cursoropen 的參數相同。  
  
> [!IMPORTANT]  
>  如果未指定 *ccopt* 值，則不論 sp_cursorprepare 中指定的 *ccopt* 值為何，預設值都是開放式。  
  
 *計數*  
 這是選擇性參數，表示要搭配 AUTO_FETCH 使用的提取緩衝區資料列數目。 預設為 20 個資料列。 當指派為輸入值與傳回值時， *rowcount*的行為會有所不同。  
  
|當做輸入值|當做傳回值|  
|--------------------|---------------------|  
|當指定 AUTO_FETCH 時，FAST_FORWARD 資料指標資料列 *計數* 代表要放入提取緩衝區中的資料列數目。|代表結果集中的資料列數目。 當指定 *scrollopt* AUTO_FETCH 值時， *rowcount* 會傳回提取緩衝區中提取的資料列數目。|  
  
 *bound_param*  
 指定選擇性使用其他參數。  
  
> [!NOTE]  
>  第五個之後的任何參數都會當做輸入參數傳遞給陳述式計畫。  
  
## <a name="code-return-value"></a>程式碼傳回值  
 *rowcount* 可能會傳回下列值。  
  
|值|描述|  
|-----------|-----------------|  
|-1|未知的資料列數目。|  
|-n|非同步擴展在作用中。|  
  
## <a name="remarks"></a>備註  
  
## <a name="scrollopt-and-ccopt-parameters"></a>scrollopt 和 ccopt 參數  
 當快取的計畫為伺服器快取優先佔用時， *scrollopt*和*ccopt*會很有用，這表示必須重新編譯識別語句的備妥控制碼。 *Scrollopt*和*ccopt*參數值必須符合 sp_cursorprepare 的原始要求中傳送的值。  
  
> [!NOTE]  
>  PARAMETERIZED_STMT 不應指派給 *scrollopt*。  
  
 當無法提供相符的值時將會導致重新編譯計劃，取消準備和執行作業。  
  
## <a name="rpc-and-tds-considerations"></a>RPC 和 TDS 考量  
 RPC RETURN_METADATA 輸入旗標可以設定為 1，要求在 TDS 資料流中傳回資料指標選取清單中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
