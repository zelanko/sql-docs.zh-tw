---
title: 自訂工作流程範例 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6a21843d147ca9faf2fa3329ca5ca81fa77171ea
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750770"
---
# <a name="custom-workflow-example-master-data-services"></a>自訂工作流程範例 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 中建立自訂的工作流程類別庫時，您要建立一個實作 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> 介面的類別。 此介面包含一個方法 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>，當工作流程啟動時，SQL Server MDS 工作流程整合服務會呼叫這個方法。 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 方法包含兩個參數：*workflowType* 包含您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之 [工作流程類型] 文字方塊中輸入的文字，而 *dataElement* 則包含觸發工作流程商務規則之項目的中繼資料和項目資料。  
  
## <a name="custom-workflow-example"></a>自訂工作流程範例  
 下列程式碼範例示範如何實作 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 方法，以便針對觸發工作流程商務規則的元素，從 XML 資料擷取 Name、Code 和 LastChgUserName 屬性，並示範如何呼叫預存程序，將這些屬性插入至其他資料庫。 如需項目資料 XML 的範例，以及所包含之標記的說明，請參閱[自訂工作流程 XML 描述 &#40;Master Data Services&#41;](create-a-custom-workflow-xml-description.md)。  
  
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
 [建立自訂工作流程 &#40;Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)  
  
  
