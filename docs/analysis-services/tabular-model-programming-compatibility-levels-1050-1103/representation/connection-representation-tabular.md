---
title: "連接表示法 （表格式） |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 4b410b16-d36e-4185-bb20-922e66e5e2b7
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fa62e16d603bb9adfff2410d14d376f358273be
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="connection-representation-tabular"></a>連接表示法 (表格式)
  定義填入表格式模型之資料來源的連接物件。  
  
## <a name="connection-representation"></a>連接表示法  
 連接物件的規格遵循 OLE DB 提供者的規則。  
  
### <a name="connection-in-amo"></a>AMO 中的連接  
 當您使用 AMO 管理表格式模型資料庫時，AMO 中的 <xref:Microsoft.AnalysisServices.DataSource> 物件與連接邏輯物件會有一對一的相符關係。  
  
 下列程式碼片段示範如何在表格式模型中建立 AMO 資料來源或連接物件。  
  
```  
  
//Create an OLEDB connection string  
StringBuilder SqlCnxStr = new StringBuilder();  
SqlCnxStr.Append(String.Format("Data Source={0};" ,SQLServer.Text));  
SqlCnxStr.Append(String.Format("Initial Catalog={0};", SQLDatabase.Text));  
SqlCnxStr.Append(String.Format("Persist Security Info={0};", false));  
SqlCnxStr.Append(String.Format("Integrated Security={0};", "SSPI"));  
SqlCnxStr.Append(String.Format("Provider={0}", "SQLNCLI11"));  
String DatasourceCnxString = SqlCnxStr.ToString();  
  
//Verify connection string and connectivity  
System.Data.OleDb.OleDbConnection OleDbCnx = new System.Data.OleDb.OleDbConnection(DatasourceCnxString);  
try  
{  
    OleDbCnx.Open();  
}  
catch ()  
{  
    throw;  
}  
String newDataSourceName = (string.IsNullOrEmpty(DataSourceName.Text) || string.IsNullOrWhiteSpace(DataSourceName.Text)) ? SQLDatabase.Text : DataSourceName.Text;  
AMO.DataSource newDatasource = newDatabase.DataSources.Add(newDataSourceName, newDataSourceName);  
newDatasource.ConnectionString = DatasourceCnxString.Text;  
if (impersonateServiceAccount.Checked)  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateServiceAccount);  
else  
{  
    if (String.IsNullOrEmpty(impersonateAccountUserName.Text))  
    {  
        MessageBox.Show(String.Format("Account User Name cannot be blank when using 'ImpersonateAccount' mode"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        return;  
    }  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateAccount, impersonateAccountUserName.Text, impersonateAccountPassword.Text);  
}  
newDatasource.Update();  
  
```  
  
## <a name="tabular-amo-2012-sample"></a>表格式 AMO 2012 範例  
 若要更了解如何使用 AMO 建立及操作連接表示法，請參閱「表格式 AMO 2012」範例的原始程式碼，特別要檢查以下的原始程式檔：Database.cs。 您可以在 Codeplex 上取得範例。 提供此範例程式碼的用意只是為了支援這裡所說明的邏輯概念，您不應將其用於生產環境。  
  
  

