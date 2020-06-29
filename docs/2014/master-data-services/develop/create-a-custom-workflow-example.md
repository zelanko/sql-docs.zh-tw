---
title: 自訂工作流程範例 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9d72e31b8e4040353c9c93bceb65ca3c2be98788
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469043"
---
# <a name="custom-workflow-example-master-data-services"></a>自訂工作流程範例 (Master Data Services)
  在中 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ，當您建立自訂工作流程類別庫時，您會建立一個可實[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender](/previous-versions/sql/sql-server-2016/hh758785(v=sql.130))介面的類別。 此介面包含一個方法[MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130))，當工作流程啟動時，SQL Server MDS 工作流程整合服務呼叫。 [MasterDataServices. WorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130))方法包含兩個參數： *workflowType*包含您在的 [**工作流程類型**] 文字方塊中輸入的文字 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] ，而*dataElement*包含觸發工作流程商務規則之專案的中繼資料和專案資料。  
  
## <a name="custom-workflow-example"></a>自訂工作流程範例  
 下列程式碼範例示範如何執行[IWorkflowTypeExtender StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130))方法，以便從觸發工作流程商務規則之專案的 XML 資料中，解壓縮名稱、程式碼和 LastChgUserName 屬性，以及如何呼叫預存程式將其插入另一個資料庫。 如需項目資料 XML 的範例，以及所包含之標記的說明，請參閱[自訂工作流程 XML 描述 &#40;Master Data Services&#41;](create-a-custom-workflow-xml-description.md)。  
  
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
  
  
