---
title: 從檔案插入影像
description: 說明如何使用來自檔案的影像。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9d80f5eec2c33fed635c18937185e2e21798e93b
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896727"
---
# <a name="inserting-an-image-from-a-file"></a>從檔案插入影像

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

視資料來源的欄位類型而定，您可以將二進位大型物件 (BLOB) 當做二進位或字元資料寫入到資料庫。 BLOB 是參考 `text`、`ntext` 與 `image` 資料類型的一般詞彙，通常包含文件與圖片。  
  
若要將 BLOB 值寫入您的資料庫，請發出適當的 INSERT 或 UPDATE 陳述式，並將 BLOB 值傳遞為輸入參數。 如果您的 BLOB 儲存為文字 (例如 SQL Server `text` 欄位)，您可以將 BLOB 以字串參數傳遞。 如果 BLOB 是以二進位格式 (例如 SQL Server `image` 欄位) 儲存的，您可以將 `byte` 類型的陣列以二進位參數方式傳遞。
  
## <a name="example"></a>範例  
下列程式碼範例會將員工資訊新增到 Northwind 資料庫的 Employees 資料表。 員工的相片會從檔案讀取，並新增至資料表中的 [相片] 欄位，也就是影像欄位。  
  
```csharp  
public static void AddEmployee(  
  string lastName,   
  string firstName,   
  string title,   
  DateTime hireDate,   
  int reportsTo,   
  string photoFilePath,   
  string connectionString)  
{  
  byte[] photo = GetPhoto(photoFilePath);  
  
  using (SqlConnection connection = new SqlConnection(  
    connectionString))  
  
  SqlCommand command = new SqlCommand(  
    "INSERT INTO Employees (LastName, FirstName, " +  
    "Title, HireDate, ReportsTo, Photo) " +  
    "Values(@LastName, @FirstName, @Title, " +  
    "@HireDate, @ReportsTo, @Photo)", connection);   
  
  command.Parameters.Add("@LastName",    
     SqlDbType.NVarChar, 20).Value = lastName;  
  command.Parameters.Add("@FirstName",   
      SqlDbType.NVarChar, 10).Value = firstName;  
  command.Parameters.Add("@Title",       
      SqlDbType.NVarChar, 30).Value = title;  
  command.Parameters.Add("@HireDate",   
       SqlDbType.DateTime).Value = hireDate;  
  command.Parameters.Add("@ReportsTo",   
      SqlDbType.Int).Value = reportsTo;  
  
  command.Parameters.Add("@Photo",  
      SqlDbType.Image, photo.Length).Value = photo;  
  
  connection.Open();  
  command.ExecuteNonQuery();  
  }  
}  
  
public static byte[] GetPhoto(string filePath)  
{  
  FileStream stream = new FileStream(  
      filePath, FileMode.Open, FileAccess.Read);  
  BinaryReader reader = new BinaryReader(stream);  
  
  byte[] photo = reader.ReadBytes((int)stream.Length);  
  
  reader.Close();  
  stream.Close();  
  
  return photo;  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 二進位和大型數值資料](sql-server-binary-large-value-data.md)
