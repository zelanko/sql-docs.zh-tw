---
title: 查詢運算式和統一資源名稱 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- query expressions
- unique resource names
- URN
ms.assetid: e0d30dbe-7daf-47eb-8412-1b96792b6fb9
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 996fad627cebc240a39337a0f0ae3a096e53901c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326178"
---
# <a name="query-expressions-and-uniform-resource-names"></a>查詢運算式和統一的資源名稱
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件 (SMO) 模型和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元會使用與 XPath 運算式類似的兩種運算式字串類型。 查詢運算式是字串，其中指定一組用來列舉物件模型階層中之一個或多個物件的準則。 統一資源名稱 (URN) 是可唯一識別單一物件的特定查詢運算式字串類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
      Object1  
      [<FilterExpression1>]/ ... /ObjectN[<FilterExpressionN>]<FilterExpression>::=  
<PropertyExpression> [and <PropertyExpression>][...n]  
  
<PropertyExpression>::=@BooleanPropertyName=true()  
 | @BooleanPropertyName=false()  
 | contains(@StringPropertyName, 'PatternString')  
  | @StringPropertyName='String'  
 | @DatePropertyName=datetime('DateString')  
 | is_null(@PropertyName)  
 | not(<PropertyExpression>)  
```  
  
## <a name="arguments"></a>引數  
 *物件*  
 指定運算式字串之該節點所代表的物件類型。 每個物件都代表這些 SMO 物件模型命名空間的集合類別：  
  
 <xref:Microsoft.SqlServer.Management.Smo>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Agent>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Mail>  
  
 <xref:Microsoft.SqlServer.Management.Dmf>  
  
 <xref:Microsoft.SqlServer.Management.Facets>  
  
 <xref:Microsoft.SqlServer.Management.RegisteredServers>  
  
 <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>  
  
 例如，您可以指定 Server 來代表 **ServerCollection** 類別，或指定 Database 來代表 **DatabaseCollection** 類別。  
  
 @*PropertyName*  
 指定與 *Object*中指定物件相關聯之類別的其中一個屬性名稱。 屬性的名稱必須以 @ 字元當做前置詞。 例如，您可以指定 @IsAnsiNull 來代表 **Database** 類別屬性 **IsAnsiNull**。  
  
 @*BooleanPropertyName*=true()  
 列舉指定之布林屬性設定為 TRUE 的所有物件。  
  
 @*BooleanPropertyName*=false()  
 列舉指定之布林屬性設定為 FALSE 的所有物件。  
  
 contains(@*StringPropertyName*, '*PatternString*')  
 列舉指定之字串屬性包含至少一個 '*PatternString*' 中指定之字元集的所有物件。  
  
 @*StringPropertyName*='*PatternString*'  
 列舉指定之字串屬性值與 '*PatternString*' 中指定之字元模式完全相同的所有物件。  
  
 @*DatePropertyName*= datetime('*DateString*')  
 列舉指定之日期屬性值與 '*DateString*' 中指定之日期相符的所有物件。 *DateString* 必須遵循格式 yyyy-mm-dd hh:mi:ss.mmm。  
  
|||  
|-|-|  
|yyyy|四位數的年份。|  
|MM|兩位數的月份 (01 到 12)。|  
|dd|兩位數的日期 (01 到 31)。|  
|hh|兩位數的小時，使用 24 小時制 (01 到 23)。|  
|mi|兩位數的分鐘 (01 到 59)。|  
|ss|兩位數的秒鐘 (01 到 59)。|  
|mmm|毫秒數 (001 到 999)。|  
  
 您可以針對儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中的任何日期格式，評估使用這種格式所指定的日期。  
  
 is_null(@*PropertyName*)  
 列舉指定之屬性具有 NULL 值的所有物件。  
  
 not(\<*PropertyExpression*>)  
 執行 *PropertyExpression*評估值的否定運算，並且列舉不符合 *PropertyExpression*中指定之條件的所有物件。 例如，not(contains(@Name, 'xyz')) 會列舉名稱中沒有 xyz 字串的所有物件。  
  
## <a name="remarks"></a>備註  
 查詢運算式是列舉 SMO 模型階層中之節點的字串。 每個節點都具有指定準則的篩選運算式，用於決定要列舉位於該節點的哪些物件。 查詢運算式是以 XPath 運算式語言建立模型。 查詢運算式會實作 XPath 所支援之運算式的小型子集，而且也具有在 XPath 中找不到的某些延伸模組。 XPath 運算式是字串，其中指定一組用來列舉 XML 文件之一個或多個標記的準則。 如需有關 XPath 的詳細資訊，請參閱 [W3C XPath Language](http://www.w3.org/TR/xpath20/)(W3C XPath 語言)。  
  
 查詢運算式必須以伺服器物件的絕對參考為開頭。 不允許使用含有前置 / 的相對運算式。 在查詢運算式中指定之物件的順序必須遵循相關聯物件模型中之集合物件的階層。 例如，在 Microsoft.SqlServer.Management.Smo 命名空間中參考物件的查詢運算式必須以伺服器節點為開頭，後面接著資料庫節點等項目。  
  
 如果未針對物件指定 *\<FilterExpression>*，就會列舉該節點上的所有物件。  
  
## <a name="uniform-resource-names-urn"></a>統一資源名稱 (URN)  
 URN 是查詢運算式的子集。 每個 URN 都會構成單一物件的完整參考。 一般的 URN 會使用 Name 屬性來識別位於每個節點的單一物件。 例如，這個 URN 會參考特定資料行：  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[@Name='SalesPerson' and @Schema='Sales']/Column[@Name='SalesPersonID']  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-enumerating-objects-using-false"></a>A. 使用 false() 列舉物件  
 這個查詢運算式會列舉在 **MyComputer** 的預設執行個體中將 **AutoClose**屬性設定為 false 的所有資料庫。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@AutoClose=false()]  
```  
  
### <a name="b-enumerating-objects-using-contains"></a>B. 使用 contains 列舉物件  
 這個查詢運算式會列舉不區分大小寫而且名稱具有 'm' 字元的所有資料庫。  
  
```  
Server[@Name='MYCOMPUTER']/Database[@CaseSensitive=false() and contains(@Name, 'm')]   
```  
  
### <a name="c-enumerating-objects-using-not"></a>C. 使用 not 列舉物件  
 這個查詢運算式會列舉不在 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] Production **結構描述中而且資料表名稱包含 History 一詞的所有** 資料表：  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[not(@Schema='Production') and contains(@Name, 'History')]  
```  
  
### <a name="d-not-supplying-a-filter-expression-for-the-final-node"></a>D. 不會為最終節點提供篩選運算式  
 這個查詢運算式會列舉 **AdventureWorks2012.Sales.SalesPerson** 資料表中的所有資料行：  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@Schema='Sales' and @Name='SalesPerson']/Columns  
```  
  
### <a name="e-enumerating-objects-using-datetime"></a>E. 使用日期時間列舉物件  
 這個查詢運算式會列舉於特定時間在 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫中建立的所有資料表：  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@CreateDate=datetime('2008-03-21 19:49:32.647')]  
```  
  
### <a name="f-enumerating-objects-using-isnull"></a>F. 使用 is_null 列舉物件  
 這個查詢運算式會列舉 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫中上次修改日期屬性沒有 NULL 的所有資料表：  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[Not(is_null(@DateLastModified))]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Invoke-PolicyEvaluation 指令程式](../database-engine/invoke-policyevaluation-cmdlet.md)   
 [SQL Server Audit &#40;Database Engine&#41;](../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
