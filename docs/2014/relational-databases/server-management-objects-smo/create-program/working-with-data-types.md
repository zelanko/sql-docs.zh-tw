---
title: 使用的資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a649e00e5b77a7b3276e82e34c04657cd8307284
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121578"
---
# <a name="working-with-data-types"></a>使用資料類型
  資料有許多類型和大小，例如已定義長度的字串、具有特定精確度的數字，或是使用者定義資料類型 (有自己的規則集合的另一個物件)。 <xref:Microsoft.SqlServer.Management.Smo.DataType>物件會分類資料的型別，以便可以正確處理[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 <xref:Microsoft.SqlServer.Management.Smo.DataType> 物件與可接受資料的物件有關聯。 下列[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Management Objects (SMO) 物件可接受必須由定義的資料<xref:Microsoft.SqlServer.Management.Smo.DataType>物件屬性：  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 接受資料之物件的 `DataType` 屬性可利用幾種方式來加以設定。  
  
-   使用預設建構函式，並指定<xref:Microsoft.SqlServer.Management.Smo.DataType>明確物件屬性  
  
-   使用多載的建構函式，並指定<xref:Microsoft.SqlServer.Management.Smo.DataType>做為參數的屬性。  
  
-   指定<xref:Microsoft.SqlServer.Management.Smo.DataType>內嵌在物件建構函式。  
  
-   使用 <xref:Microsoft.SqlServer.Management.Smo.DataType> 類別的其中一個靜態成員，例如 `Int`。 事實上，這樣會傳回 <xref:Microsoft.SqlServer.Management.Smo.DataType> 物件的執行個體。  
  
 <xref:Microsoft.SqlServer.Management.Smo.DataType> 物件有好幾個屬性會定義資料的類型。 例如，<xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 屬性會指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 常數值，代表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料類型會列在<xref:Microsoft.SqlServer.Management.Smo.SqlDataType>列舉型別。 這是指像是 `varchar`、`nchar`、`currency`、`integer`、`float` 和 `datetime` 等資料類型。  
  
 當建立該資料類型時，必須為資料設定特定的屬性。 例如，如果它是 `nchar` 類型，字串資料的長度必須在 `Length` 屬性中設定。 這同樣適用於數值，您必須為數值指定有效位數及小數位數。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 和 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 資料類型指的是包含使用者定義之資料類型定義的物件。 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 是根據 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 列舉中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型。 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>根據[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET 資料型別。 一般來說，這些代表特定類型的資料，資料庫會因為組織所定義的商務規則而經常重複使用這些資料。 例如，儲存金錢數量和貨幣單位的資料類型對於處理多種貨幣的公司會很有幫助。  
  
 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>列舉型別包含一份所有[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-支援的資料類型。  
  
## <a name="examples"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>在 Visual Basic 中使用建構函式內的規格來建構 DataType 物件  
 此程式碼範例示範如何使用建構函式建立會根據不同的資料類型的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 和 XML 類型全都需要一個名稱值，才能識別此物件。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes1](SMO How to#SMO_VBDataTypes1)]  -->  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>在 Visual C# 中使用建構函式內的規格來建構 DataType 物件  
 此程式碼範例示範如何使用建構函式建立會根據不同的資料類型的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 和 XML 類型全都需要一個名稱值，才能識別此物件。  
  
```  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguements specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>在 Visual Basic 中使用預設建構函式來建構 DataType 物件  
 此程式碼範例示範如何建立會根據不同的資料類型的執行個體使用預設建構函式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。 然後會使用這些屬性來指定資料類型。  
  
 **附註** <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>， <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>，和 XML 類型全都需要一個名稱值來識別物件。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes2](SMO How to#SMO_VBDataTypes2)]  -->  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>在 Visual C# 中使用預設建構函式來建構 DataType 物件  
 此程式碼範例示範如何建立會根據不同的資料類型的執行個體使用預設建構函式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料型別。 然後會使用這些屬性來指定資料類型。  
  
 **附註** <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>， <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>，和 XML 類型全都需要一個名稱值來識別物件。  
  
```  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
