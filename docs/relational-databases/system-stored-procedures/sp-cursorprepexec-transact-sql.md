---
title: sp_cursorprepexec （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 660a75f1e6fea9b5a825372501c2e65f2dd3874b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "69652430"
---
# <a name="sp_cursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  編譯提交之資料指標陳述式或批次的計畫，然後建立及擴展資料指標。 sp_cursorprepexec 結合 sp_cursorprepare 和 sp_cursorexecute 的功能。 這個程式的叫用方式是在表格式資料流程（TDS）封包中指定 ID = 5。  
  
 ![連結圖示](../../database-engine/configure-windows/media/topic-link.gif "連結圖示") [transact-sql 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
    [, '@parameter_name[,...n ]']
```  
  
## <a name="arguments"></a>引數  
 *備妥的控制碼*  
 是產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的已備妥*控制碼*識別碼。 需要備妥的*控制碼*，並傳回**int**。  
  
 *cursor*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的資料指標識別碼。 資料*指標*是必要的參數，必須在所有作用於此資料指標的後續程式上提供，例如 sp_cursorfetch。  
  
 *化*  
 識別參數化的陳述式。 變數的*params*定義會取代語句中的參數標記。 *params*是針對**Ntext**、 **Nchar**或**Nvarchar**輸入值呼叫的必要參數。  
  
> [!NOTE]  
>  當*stmt*參數化且*scrollopt* PARAMETERIZED_STMT 值為 ON 時，請使用**Ntext**字串做為輸入值。  
  
 *句*  
 定義資料指標結果集。 *語句*參數是必要的，而且會呼叫**Ntext**、 **Nchar**或**Nvarchar**輸入值。  
  
> [!NOTE]  
>  指定 stmt 值的規則與 sp_cursoropen 相同，唯一的例外是*stmt*字串資料類型必須是**Ntext**。  
  
 *選項*  
 傳回資料指標結果集資料行描述的選擇性參數。 * 選項需要下列**int**輸入值。  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 捲動選項。 *scrollopt*是需要下列其中一個**int**輸入值的選擇性參數。  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 因為要求的選項不適合* \<stmt>* 所定義的資料指標，所以這個參數會同時做為輸入和輸出。 在這類情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指派適合的類型並修改這個值。  
  
 *ccopt*  
 並行控制選項。 *ccopt*是需要下列其中一個**int**輸入值的選擇性參數。  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (之前稱為 LOCKCC)|  
|0x0004|**開放式**（先前稱為 OPTCC）|  
|0x0008|OPTIMISTIC (之前稱為 OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 如同*scrollpt*， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以指派與要求的值不同的值。  
  
 *計數*  
 這是選擇性參數，表示要搭配 AUTO_FETCH 使用的提取緩衝區資料列數目。 預設為 20 個資料列。 指派為輸入值與傳回值時，資料列*計數*的行為會有所不同。  
  
|當做輸入值|當做傳回值|  
|--------------------|---------------------|  
|當指定 AUTO_FETCH 時，FAST_FORWARD 的資料指標資料列*計數*代表要放入提取緩衝區中的資料列數目。|代表結果集中的資料列數目。 當指定了*scrollopt* AUTO_FETCH 值時， *rowcount*會傳回提取緩衝區中提取的資料列數目。|  

*parameter_name*指定一個或多個參數名稱，如 params 引數中所定義。  Params 中包含的每個參數都必須提供參數。 當 params 中的 Transact-sql 語句或批次未定義任何參數時，不需要這個引數。
  
## <a name="return-code-values"></a>傳回碼值  
 如果 params 傳回 Null 值，則語句不會參數化。  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorexecute &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursorprepare &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
