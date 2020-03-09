---
title: FILESTREAM 資料
description: 描述如何使用以 FILESTREAM 屬性儲存在 SQL Server 2008 中的大型值資料。
ms.date: 08/15/2019
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e3e26a76522d1c1a99794076c5f152e6ec1e1f7d
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896746"
---
# <a name="filestream-data"></a>FILESTREAM 資料

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

FILESTREAM 儲存體屬性適用於儲存在 varbinary(max) 資料行中的二進位 (BLOB) 資料。 在 FILESTREAM 之前，需要特殊處理才能儲存二進位資料。 非結構化資料 (例如文字文件、影像與影片) 通常會儲存在資料庫外部，因此難以管理。

> [!NOTE]
> 您必須安裝 .NET Framework 3.5 SP1 (或更新版本) 或 .NET Core，才能使用 SqlClient 來處理 FILESTREAM 資料。

針對 varbinary(max) 資料行指定 FILESTREAM 屬性會導致 SQL Server 將資料儲存在本機 NTFS 檔案系統上，而非資料庫檔案中。 雖然系統會以不同的方式儲存資料，但是您可以使用支援使用 varbinary(max) 資料 (儲存在資料庫中) 的相同 Transact-SQL 陳述式。

## <a name="sqlclient-support-for-filestream"></a>FILESTREAM 的 SqlClient 支援

Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) 支援使用 <xref:System.Data.SqlTypes> 命名空間中定義的 <xref:Microsoft.Data.SqlTypes.SqlFileStream> 類別來讀取和寫入 FILESTREAM 資料。 `SqlFileStream` 繼承自 <xref:System.IO.Stream> 類別，其提供讀取和寫入至資料流的方法。 從資料流讀取會將資料從資料流傳輸到資料結構中，例如位元組陣列。 寫入會將資料從資料結構傳輸到資料流。

### <a name="creating-the-sql-server-table"></a>建立 SQL Server 資料表

下列 Transact-SQL 陳述式會建立名為 employees 的資料表並插入一個資料列。 啟用 FILESTREAM 儲存體之後，您可以使用此資料表搭配後面的程式碼範例。 《SQL Server 線上叢書》中資源的連結位於本主題的結尾。

```sql
CREATE TABLE employees
(
  EmployeeId INT  NOT NULL  PRIMARY KEY,
  Photo VARBINARY(MAX) FILESTREAM  NULL,
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL
  UNIQUE DEFAULT NEWID()
)
GO
Insert into employees
Values(1, 0x00, default)
GO
```

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>範例：讀取、覆寫及插入 FILESTREAM 資料

下列範例示範如何從 FILESTREAM 讀取資料。 程式碼會取得檔案的邏輯路徑，將 `FileAccess` 設定為 `Read`，並將 `FileOptions` 設為 `SequentialScan`。 接著程式碼會從 SqlFileStream 將位元組讀取到緩衝區中。 然後，這些位元組會寫入至主控台視窗。

此範例也會示範如何將資料寫入至 FILESTREAM，以覆寫所有現有資料。 此程式碼會取得檔案的邏輯路徑，並建立 `SqlFileStream`，將 `FileAccess` 設定為 `Write`，將 `FileOptions` 設定為 `SequentialScan`。 單一位元組會寫入至 `SqlFileStream`，並取代檔案中的任何資料。

此範例還會示範如何使用 Seek 方法來附加資料至檔案的結尾，藉以將資料寫入 FILESTREAM。 此程式碼會取得檔案的邏輯路徑，並建立 `SqlFileStream`，將 `FileAccess` 設定為 `ReadWrite`，將 `FileOptions` 設定為 `SequentialScan`。 程式碼會使用 Seek 方法搜尋檔案結尾，並將單一位元組附加至現有的檔案。

```csharp
using System;
using Microsoft.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;
using System.IO;

namespace FileStreamTest
{
    class Program
    {
        static void Main(string[] args)
        {
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");
            ReadFileStream(builder);
            OverwriteFileStream(builder);
            InsertFileStream(builder);

            Console.WriteLine("Done");
        }

        private static void ReadFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for the file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Read the contents as bytes and write them to the console
                            for (long index = 0; index < fileStream.Length; index++)
                            {
                                Console.WriteLine(fileStream.ReadByte());
                            }
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void OverwriteFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Write a single byte to the file. This will
                            // replace any data in the file.
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void InsertFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.ReadWrite, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Seek to the end of the file
                            fileStream.Seek(0, SeekOrigin.End);

                            // Append a single byte
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }

        }
    }
}
```

如需其他範例，請參閱[如何儲存二進位資料並將其擷取至檔案資料流資料行](https://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str)。

## <a name="resources-in-sql-server-books-online"></a>《SQL Server 線上叢書》中的資源

FILESTREAM 的完整文件位於《SQL Server 線上叢書》中的下列章節。

|主題|描述|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)|說明使用 FILESTREAM 儲存體的時機，以及該儲存體如何將 SQL Server 資料庫引擎與 NTFS 檔案系統整合。|
|[建立 FILESTREAM 資料的用戶端應用程式](../../../relational-databases/blob/create-client-applications-for-filestream-data.md)|說明用來處理 FILESTREAM 資料的 Windows API 函式。|
|[FILESTREAM 和其他 SQL Server 功能](../../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)|提供搭配 SQL Server 其他功能使用 FILESTREAM 資料的考量、指導方針與限制。|

## <a name="next-steps"></a>後續步驟
- [SQL Server 資料類型和 ADO.NET](sql-server-data-types.md)
- [SQL Server 二進位和大型數值資料](sql-server-binary-large-value-data.md)
