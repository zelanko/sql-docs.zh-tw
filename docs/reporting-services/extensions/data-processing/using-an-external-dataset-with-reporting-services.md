---
title: "透過 Reporting Services 使用外部資料集 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- DataSet objects [Reporting Services]
- data processing extensions [Reporting Services], custom DataSet objects
- custom DataSet objects [Reporting Services]
- external DataSet objects [Reporting Services]
ms.assetid: 11daa013-ec17-4760-80e3-6d84cd8d5722
caps.latest.revision: "49"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 179c1ecb3641a848561c49489d1d23a51c1b6ff8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="using-an-external-dataset-with-reporting-services"></a>透過 Reporting Services 使用外部資料集
  **DataSet** 物件是支援 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 已中斷連線之分散式資料案例的關鍵。 **DataSet** 物件是常駐記憶體的資料表示，可提供與資料來源無關的一致性關聯式程式設計模型。 它可與多個不同的資料來源一起使用、與 XML 資料一起使用，或管理應用程式的本機資料。 **DataSet** 物件表示一組完整的資料，包括相關資料表、條件約束及資料表間的關聯性。 因為 **DataSet** 物件具有儲存和公開資料的多樣性，所以通常會在報告您的資料之前，先將該資料處理和轉換成 **DataSet** 物件。  
  
 透過 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組，您可以整合由外部應用程式建立的任何自訂 **DataSet** 物件。 若要完成這項動作，您可以在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中建立自訂資料處理延伸模組，以作為 **DataSet** 物件與報表伺服器之間的橋樑。 大部分處理這個 **DataSet** 物件的程式碼，都是包含在您建立的 **DataReader** 類別中。  
  
 向報表伺服器公開 **DataSet** 物件的第一個步驟，是在可以擴展 **DataSet** 物件的 **DataReader** 類別中，為提供者實作特定方法。 下列範例示範如何使用 **DataReader** 類別中的提供者特定方法，將靜態資料載入 **DataSet** 物件。  
  
```vb  
'Private members of the DataReader class  
Private m_dataSet As System.Data.DataSet  
Private m_currentRow As Integer  
  
'Method to create a dataset  
Friend Sub CreateDataSet()  
   ' Create a dataset.  
   Dim ds As New System.Data.DataSet("myDataSet")  
   ' Create a data table.   
   Dim dt As New System.Data.DataTable("myTable")  
   ' Create a data column and set various properties.   
   Dim dc As New System.Data.DataColumn()  
   dc.DataType = System.Type.GetType("System.Decimal")  
   dc.AllowDBNull = False  
   dc.Caption = "Number"  
   dc.ColumnName = "Number"  
   dc.DefaultValue = 25  
   ' Add the column to the table.   
   dt.Columns.Add(dc)  
   ' Add 10 rows and set values.   
   Dim dr As System.Data.DataRow  
   Dim i As Integer  
   For i = 0 To 9  
      dr = dt.NewRow()  
      dr("Number") = i + 1  
      ' Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr)  
   Next i  
  
   ' Fill the dataset.  
   ds.Tables.Add(dt)  
  
   ' Use a private variable to store the dataset in your  
   ' DataReader.  
   m_dataSet = ds  
  
   ' Set the current row to -1.  
   m_currentRow = - 1  
End Sub 'CreateDataSet  
```  
  
```csharp  
// Private members of the DataReader class  
private System.Data.DataSet m_dataSet;  
private int m_currentRow;  
  
// Method to create a dataset  
internal void CreateDataSet()  
{  
   // Create a dataset.  
   System.Data.DataSet ds = new System.Data.DataSet("myDataSet");  
   // Create a data table.   
   System.Data.DataTable dt = new System.Data.DataTable("myTable");  
   // Create a data column and set various properties.   
   System.Data.DataColumn dc = new System.Data.DataColumn();   
   dc.DataType = System.Type.GetType("System.Decimal");   
   dc.AllowDBNull = false;   
   dc.Caption = "Number";   
   dc.ColumnName = "Number";   
   dc.DefaultValue = 25;   
   // Add the column to the table.   
   dt.Columns.Add(dc);   
   // Add 10 rows and set values.   
   System.Data.DataRow dr;   
   for(int i = 0; i < 10; i++)  
   {   
      dr = dt.NewRow();   
      dr["Number"] = i + 1;   
      // Be sure to add the new row to the DataRowCollection.   
      dt.Rows.Add(dr);  
   }  
  
   // Fill the dataset.  
   ds.Tables.Add(dt);  
  
   // Use a private variable to store the dataset in your  
   // DataReader.  
   m_dataSet = ds;  
  
   // Set the current row to -1.  
   m_currentRow = -1;  
}  
```  
  
```csharp  
public bool Read()  
{  
   m_currentRow++;  
   if (m_currentRow >= m_dataSet.Tables[0].Rows.Count)   
   {  
      return (false);  
   }   
   else   
   {  
      return (true);  
   }  
}  
  
public int FieldCount  
{  
   // Return the count of the number of columns, which in  
   // this case is the size of the column metadata  
   // array.  
   get { return m_dataSet.Tables[0].Columns.Count; }  
}  
  
public string GetName(int i)  
{  
   return m_dataSet.Tables[0].Columns[i].ColumnName;  
}  
  
public Type GetFieldType(int i)  
{  
   // Return the actual Type class for the data type.  
   return m_dataSet.Tables[0].Columns[i].DataType;  
}  
  
public Object GetValue(int i)  
{  
   return m_dataSet.Tables[0].Rows[m_currentRow][i];  
}  
  
public int GetOrdinal(string name)  
{  
   // Look for the ordinal of the column with the same name and return it.  
   // Returns -1 if not found.  
   return m_dataSet.Tables[0].Columns[name].Ordinal;  
}  
```  
  
 一旦您建立或是擷取資料集，就可以在實作 **DataReader** 類別的 **Read**、**GetValue**、**GetName**、**GetOrdinal**、**GetFieldType** 和 **FieldCount** 成員時，使用 **DataSet** 物件。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
