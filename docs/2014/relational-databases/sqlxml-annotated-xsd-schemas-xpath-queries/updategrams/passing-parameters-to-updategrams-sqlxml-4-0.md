---
title: 將參數傳遞至 Updategram （SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 92238e27c364c8f09721a55d00c750022b53a18f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66014727"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>將參數傳遞至 Updategrams (SQLXML 4.0)
  Updategrams 是範本，所以您可以將參數傳遞給它們。 如需將參數傳遞至範本的詳細資訊，請參閱[Updategram &#40;SQLXML 4.0&#41;的安全性考慮](../security/updategram-security-considerations-sqlxml-4-0.md)。  
  
 Updategrams 可讓您將 NULL 當做參數值來傳遞。 若要傳遞 NULL 參數值，您會指定 `nullvalue` 屬性。 然後會將指派給 `nullvalue` 屬性的值當做參數值來提供。 Updategrams 將此值視為 NULL。  
  
> [!NOTE]  
>  在 `<sql:header>` 和 `<updg:header>` 中，您應該將 `nullvalue` 指定為不合格；但是在 `<updg:sync>` 中，您應該將 `nullvalue` 指定為合格 (例如 `updg:nullvalue`)。  
  
## <a name="examples"></a>範例  
 若要使用下列範例建立工作範例，您必須符合[執行 SQLXML 範例的需求](../../sqlxml/requirements-for-running-sqlxml-examples.md)中所指定的需求。  
  
 使用 Updategram 範例之前，請注意下列事項：  
  
-   此範例會使用預設對應 (也就是說，updategram 中不會指定任何對應結構描述)。 如需使用對應架構之 updategram 的更多範例，請參閱[在 Updategram 中指定批註式對應架構 &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. 傳遞參數給 updategram  
 在此範例中，updategram 會變更 umanResources.Shift 資料表內員工的姓氏。 有兩個參數會傳遞給 updategram：用來唯一識別移位的 ShiftID 及 Name。  
  
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
  
2.  在中準備 SQLXML 4.0 測試腳本（Sqlxml4test.vbs），以[使用 ADO 執行 sqlxml 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)來執行 updategram，方法是在之後新增下列幾行`cmd.Properties("Output Stream").Value = outStream`：  
  
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
  
2.  在中準備 SQLXML 4.0 測試腳本（Sqlxml4test.vbs），以[使用 ADO 執行 sqlxml 4.0 查詢](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)來執行 updategram，方法是在之後新增下列幾行`cmd.Properties("Output Stream").Value = outStream`：  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
