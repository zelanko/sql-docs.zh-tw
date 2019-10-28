---
title: 從檔案插入影像
description: 說明如何使用檔案中的影像。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8f7b561a6aba4539964d73dacfd9e45db2dd6aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452172"
---
# <a name="inserting-an-image-from-a-file"></a>從檔案插入影像

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

視資料來源的欄位類型而定，您可以將二進位大型物件（BLOB）當做二進位或字元資料寫入資料庫中。 BLOB 是參考 `text`、`ntext` 和 `image` 資料類型的一般詞彙，通常包含檔和圖片。  
  
若要將 BLOB 值寫入您的資料庫，請發出適當的 INSERT 或 UPDATE 陳述式，並將 BLOB 值傳遞為輸入參數。 如果您的 BLOB 儲存為文字（例如 SQL Server `text` 欄位），您可以將 BLOB 當做字串參數傳遞。 如果 BLOB 是以二進位格式儲存（例如 SQL Server `image` 欄位），您可以將 `byte` 類型的陣列傳遞為二進位參數。
  
## <a name="example"></a>範例  
下列程式碼範例會將員工資訊加入至 Northwind 資料庫的 Employees 資料表。 員工的相片會從檔案讀取，並加入至資料表中的 [相片] 欄位，也就是影像欄位。  
  
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
