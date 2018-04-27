---
title: distinct-values 函數 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
caps.latest.revision: 26
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2d83e7cad7352e48576a29144f3cff1603b2e0c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="functions-on-sequences---distinct-values"></a>序列的相異值的函式
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除重複值所指定的時序 *$arg*。 如果 *$arg*是空的序列，則函數會傳回空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 不可部份完成值的時序。  
  
## <a name="remarks"></a>備註  
 所有類型的不可部份完成值傳遞至**distinct-values （)** 必須是相同的基底類型的子類型。 接受的基底類型的類型，可支援**eq**作業。 這些類型包含三個內建數值基底類型以及日期/時間基底類型，它們是 xs:string、xs:boolean 以及 xdt:untypedAtomic。 xdt:untypedAtomic 類型的值會轉換成 xs:string。 如果混合了這些類型，或是如果傳遞了其他類型的值，就會引發靜態錯誤。  
  
 結果**distinct-values （)** 包含原始基數接收傳入的類型，例如 xdt，xs: string 的基底類型。 如果輸入是靜態空白，則會隱含空白並引發靜態錯誤。  
  
 xs:string 類型的值將與 XQuery 預設的「Unicode 字碼指標定序」相比較。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. 使用 distinct-values() 函數以移除時序的重複值  
 在此範例中，XML 執行個體，其中包含電話號碼指派給**xml**類型變數。 針對此變數會使用指定之 XQuery **distinct-values （)** 編譯不包含重複的電話號碼清單的函式。  
  
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
  
 下列查詢中，在一連串的數字 （1，1，2） 會在傳遞至**distinct-values （)** 函式。 該函數接著會移除序列中的重複並傳回另兩個。  
  
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
  
-   **Distinct-values （)** 函式會將整數值對應至 xs: decimal。  
  
-   **Distinct-values （)** 函式只支援先前提及的類型，並不支援的基底類型的混合。  
  
-   **Distinct-values （)** 不支援在 xs: duration 值上的函式。  
  
-   不支援提供定序的語法選項。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
