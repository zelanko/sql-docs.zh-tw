---
title: 相異值函數（XQuery） |Microsoft Docs
description: 瞭解如何使用 XQuery 中的相異值函式，從序列中移除重複的值。
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a82bfef35b0d8aec39f7f539f65e6ff1fe8f3ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753570"
---
# <a name="functions-on-sequences---distinct-values"></a>序列的相關函式 - distinct-values
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

  從 *$arg*所指定的順序中移除重複的值。 如果 *$arg*是空的序列，函數會傳回空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 不可部份完成值的時序。  
  
## <a name="remarks"></a>備註  
 傳遞給**相異值（）** 的所有不可部分完成數值型別，必須是相同基底類型的子類型。 接受的基底類型是支援**eq**運算的類型。 這些類型包含三個內建數值基底類型以及日期/時間基底類型，它們是 xs:string、xs:boolean 以及 xdt:untypedAtomic。 xdt:untypedAtomic 類型的值會轉換成 xs:string。 如果混合了這些類型，或是如果傳遞了其他類型的值，就會引發靜態錯誤。  
  
 **相異值（）** 的結果會收到傳入類型的基底類型，例如 Xdt： untypedAtomic 的案例中的 xs： string，以及原始基數。 如果輸入是靜態空白，則會隱含空白並引發靜態錯誤。  
  
 xs:string 類型的值將與 XQuery 預設的「Unicode 字碼指標定序」相比較。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. 使用 distinct-values() 函數以移除時序的重複值  
 在此範例中，會將包含電話號碼的 XML 實例指派給**xml**類型變數。 針對這個變數所指定的 XQuery 會使用**相異值（）** 函數來編譯不包含重複專案的電話號碼清單。  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 以下是結果：  
  
```  
111-111-1111 222-222-2222    
```  
  
 在下列查詢中，會將一連串的數位（1，1，2）傳入**相異值（）** 函數。 該函數接著會移除序列中的重複並傳回另兩個。  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 此查詢傳回 1 2。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **相異值（）** 函數會將整數值對應至 xs： decimal。  
  
-   **相異值（）** 函數只支援先前提到的類型，而且不支援混合基底類型。  
  
-   不支援 xs： duration 值上的**相異值（）** 函數。  
  
-   不支援提供定序的語法選項。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
