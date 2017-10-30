---
title: "保存自訂物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom objects [Integration Services], persisting
ms.assetid: 97c19716-6447-4c1c-b277-cc2e6c1e6a6c
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7b43f65b19f3dd4804ba1f7c18a81b640ed277d5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="persisting-custom-objects"></a>保存自訂物件
  您不需要您建立，只要它們的屬性使用例如只有簡單資料類型的自訂物件實作自訂持續性**整數**和**字串**。 預設的持續性實作可以儲存物件的中繼資料，及其所有屬性值。  
  
 不過，如果您的物件具有使用複雜資料類型的屬性，或是如果您想要在載入和儲存屬性值時，在它們上面執行自訂處理，可以實作 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist> 介面及其 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.LoadFromXML%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.SaveToXML%2A> 方法。 在這些方法中，您從封裝的 XML 定義載入 XML 片段 (或是將它儲存到封裝的 XML 定義)，而 XML 片段包含物件的屬性以及其目前的值。 並未定義這個 XML 片段的格式，它必須只能是格式正確的 XML。  
  
> [!IMPORTANT]  
>  當您實作自訂持續性時，必須保存物件的所有屬性，包括繼承的屬性和您加入的自訂屬性。  
  
## <a name="example"></a>範例  
 雖然 Sql Server 自訂連接管理員範例不需要三個屬性類型的自訂持續性**字串**，下列程式碼顯示將需要保存連接管理員及其屬性的自訂程式碼範例。 包含此程式碼的類別必須實作 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist> 介面。  
  
```vb  
Private Const PERSIST_ELEMENT As String = "SqlConnectionManager"  
Private Const PERSIST_SERVER As String = "Server"  
Private Const PERSIST_DATABASE As String = "Database"  
Private Const PERSIST_CONNECTIONSTRING As String = "ConnectionString"  
  
Public Sub LoadFromXML(ByVal node As System.Xml.XmlElement, _  
  ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) _  
  Implements Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.LoadFromXML  
  
  Dim propertyNode As XmlNode  
  
  ' Make sure that the correct node is being loaded.  
  If node.Name <> PERSIST_ELEMENT Then  
    Throw New Exception("Persisted element is not of type " & PERSIST_ELEMENT)  
  End If  
  
  ' Load the three properties of the object from XML into variables.  
  For Each propertyNode In node.ChildNodes  
    Select Case propertyNode.Name  
      Case PERSIST_SERVER  
        _serverName = propertyNode.InnerText  
      Case PERSIST_DATABASE  
        _databaseName = propertyNode.InnerText  
      Case PERSIST_CONNECTIONSTRING  
        _connectionString = propertyNode.InnerText  
    End Select  
  Next  
  
End Sub  
  
Public Sub SaveToXML(ByVal doc As System.Xml.XmlDocument, _  
  ByVal infoEvents As Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents) _  
  Implements Microsoft.SqlServer.Dts.Runtime.IDTSComponentPersist.SaveToXML  
  
  Dim elementRoot As XmlElement  
  Dim propertyNode As XmlNode  
  
  ' Create a new node to persist the object and its properties.  
  elementRoot = doc.CreateElement(String.Empty, PERSIST_ELEMENT, String.Empty)  
  
  ' Save the three properties of the object from variables into XML.  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_SERVER, String.Empty)  
  propertyNode.InnerText = _serverName  
  elementRoot.AppendChild(propertyNode)  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_DATABASE, String.Empty)  
  propertyNode.InnerText = _databaseName  
  elementRoot.AppendChild(propertyNode)  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_CONNECTIONSTRING, String.Empty)  
  propertyNode.InnerText = _connectionString  
  elementRoot.AppendChild(propertyNode)  
  
  doc.AppendChild(elementRoot)  
  
End Sub  
```  
  
```csharp  
private const string PERSIST_ELEMENT = "SqlConnectionManager";  
private const string PERSIST_SERVER = "Server";  
private const string PERSIST_DATABASE = "Database";  
private const string PERSIST_CONNECTIONSTRING = "ConnectionString";  
  
public void LoadFromXML(System.Xml.XmlElement node,  
  Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  // Make sure that the correct node is being loaded.  
  if (node.Name != PERSIST_ELEMENT)  
  {  
    throw new Exception("Persisted element is not of type " + PERSIST_ELEMENT);  
  }  
  
  // Save the three properties of the object from variables into XML.  
  foreach (XmlNode propertyNode in node.ChildNodes)  
  {  
    switch (propertyNode.Name)  
    {  
      case PERSIST_SERVER:  
        _serverName = propertyNode.InnerText;  
        break;  
      case PERSIST_DATABASE:  
        _databaseName = propertyNode.InnerText;  
        break;  
      case PERSIST_CONNECTIONSTRING:  
        _connectionString = propertyNode.InnerText;  
        break;  
    }  
  }  
  
}  
  
public void SaveToXML(System.Xml.XmlDocument doc,  
  Microsoft.SqlServer.Dts.Runtime.IDTSInfoEvents infoEvents)  
{  
  
  XmlElement elementRoot;  
  XmlNode propertyNode;  
  
  // Create a new node to persist the object and its properties.  
  elementRoot = doc.CreateElement(String.Empty, PERSIST_ELEMENT, String.Empty);  
  
  // Save the three properties of the object from variables into XML.  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_SERVER, String.Empty);  
  propertyNode.InnerText = _serverName;  
  elementRoot.AppendChild(propertyNode);  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_DATABASE, String.Empty);  
  propertyNode.InnerText = _databaseName;  
  elementRoot.AppendChild(propertyNode);  
  
  propertyNode = doc.CreateNode(XmlNodeType.Element, PERSIST_CONNECTIONSTRING, String.Empty);  
  propertyNode.InnerText = _connectionString;  
  elementRoot.AppendChild(propertyNode);  
  
  doc.AppendChild(elementRoot);  
  
}  
```  
 
## <a name="see-also"></a>另請參閱  
 [開發 Integration Services 自訂物件](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [自訂物件的建立、部署和偵錯](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
  

