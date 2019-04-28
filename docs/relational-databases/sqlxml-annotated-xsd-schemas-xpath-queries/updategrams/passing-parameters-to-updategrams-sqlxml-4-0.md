---
title: 將參數傳遞給 Updategram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 501ee9f2bde6d77e8f07fcbdfa6a43a0fa6f3b3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007300"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>將參數傳遞至 Updategrams (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Updategrams 是範本，所以您可以將參數傳遞給它們。 如需參數傳遞給範本的詳細資訊，請參閱[Updategram 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)。  
  
 Updategrams 可讓您將 NULL 當做參數值來傳遞。 若要傳遞 NULL 參數值，指定**nullvalue**屬性。 值，指派給**nullvalue**屬性則提供做為參數值。 Updategrams 將此值視為 NULL。  
  
> [!NOTE]  
>  在 **\<sql:header >** 並 **\<updg:header >**，您應該指定**nullvalue**為不合格; 但是，請在**\<updg:sync >**，您指定**nullvalue**為合格 (例如**updg: nullvalue**)。  
  
## <a name="examples"></a>範例  
 若要建立使用下列範例的實用範例，您必須符合指定的需求[如需執行 SQLXML 範例的需求](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
 使用 Updategram 範例之前，請注意下列事項：  
  
-   此範例會使用預設對應 (也就是說，updategram 中不會指定任何對應結構描述)。 如需使用對應結構描述的 updategram 的範例，請參閱[在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. 傳遞參數給 updategram  
 在此範例中，updategram 會變更 umanResources.Shift 資料表內員工的姓氏。 Updategram 會傳遞兩個參數：ShiftID，用來唯一識別移位和名稱。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  將上述的 updategram 複製到 [記事本] 中，並將它儲存為 UpdategramWithParameters.xml 檔。  
  
2.  準備中的 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) [Ba6e326154d2"&gt;using ADO to Execute SQLXML 4.0 Queries&lt](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)以加入下列幾行之後執行 updategram `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. 將 NULL 當做 updategram 的參數值來傳遞  
 在執行 updategram 時，"isnull" 值會指派給您想要設定為 NULL 的參數。 Updategram 會將 "isnulll" 參數值轉換成 NULL，並適當地加以處理。  
  
 下列 updategram 會將員工職稱設定為 NULL：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  將上述的 updategram 複製到 [記事本] 中，並將它儲存為 UpdategramPassingNullvalues.xml 檔。  
  
2.  準備中的 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) [Ba6e326154d2"&gt;using ADO to Execute SQLXML 4.0 Queries&lt](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)以加入下列幾行之後執行 updategram `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
