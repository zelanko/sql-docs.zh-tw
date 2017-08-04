---
title: "自訂工作流程範例 (Master Data Services) |Microsoft 文件"
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
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2b3ad5ab349456364d2aa0af8826dd6970e55b1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---example"></a>建立自訂工作流程的範例
  在[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]，當您建立自訂工作流程類別庫，您建立實作 Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender 介面的類別。 此介面包含一個方法 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>，當工作流程啟動時，SQL Server MDS 工作流程整合服務會呼叫這個方法。 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>方法包含兩個參數： *workflowType*包含您在輸入的文字**工作流程類型**文字方塊中[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]，和*dataelement 轉換*包含觸發工作流程商務規則之項目的中繼資料和項目資料。  
  
## <a name="custom-workflow-example"></a>自訂工作流程範例  
 下列程式碼範例示範如何實作 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 方法，以便針對觸發工作流程商務規則的元素，從 XML 資料擷取 Name、Code 和 LastChgUserName 屬性，並示範如何呼叫預存程序，將這些屬性插入至其他資料庫。 如需範例的項目資料 XML 和它所包含之標記的說明，請參閱[自訂工作流程 XML 描述 &#40;Master Data services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂工作流程 &#40;Master Data services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
