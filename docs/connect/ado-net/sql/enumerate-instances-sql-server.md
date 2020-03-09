---
title: 列舉 SQL Server 的執行個體 (ADO.NET)
description: 說明如何列舉 SQL Server 的使用中執行個體。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: bd0dbbedcb2fa33af80e0a1a1d593bf7df27edb6
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896952"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>列舉 SQL Server 的執行個體 (ADO.NET)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 允許應用程式在目前網路內尋找 SQL Server 執行個體。 <xref:System.Data.Sql.SqlDataSourceEnumerator> 類別會向應用程式開發人員公開此資訊，並提供包含所有可見伺服器相關資訊的 <xref:System.Data.DataTable>。 這個傳回的資料表包含網路上可用伺服器執行個體的清單 (該清單與使用者嘗試建立新連線時所提供的清單相符)，並展開包含 [連線屬性]  對話方塊上所有可用伺服器的下拉式清單。 顯示的結果不一定完整。  
  
> [!NOTE]
>  就像大多數的 Windows 服務一樣，最好以最少的可能權限來執行 SQL Browser 服務。 如需 SQL Browser 服務及如何管理其行為的詳細資訊，請參閱《SQL Server 線上叢書》。  
  
## <a name="retrieving-an-enumerator-instance"></a>擷取列舉程式執行個體  
若要擷取包含可用 SQL Server 執行個體相關資訊的資料表，您必須先使用共用/靜態 <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A> 屬性擷取列舉值：  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
一旦您擷取靜態執行個體之後，就可以呼叫 <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A> 方法，來傳回包含可用伺服器相關資訊的 <xref:System.Data.DataTable>：  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
從方法呼叫傳回的資料表會包含下列資料行，這些資料行全都包含 `string` 值：  
  
|資料行|描述|  
|------------|-----------------|  
|**ServerName**|伺服器的名稱。|  
|**InstanceName**|伺服器執行個體的名稱。 如果伺服器是以預設執行個體的形式執行，則為空白。|  
|**IsClustered**|指出伺服器是否為叢集的一部分。|  
|**版本**|伺服器的版本。 例如：<br /><br /> -   9.00.x (SQL Server 2005)<br />-   10.0.xx (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />-   11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>列舉限制  
不一定會列出所有可用的伺服器。 清單可能會根據各種因素 (例如，逾時和網路流量) 而有所不同。 這可能導致清單在兩次連續呼叫中都不一樣。 只會列出相同網路上的伺服器。 廣播封包通常不會周遊路由器，這就是為什麼您可能看不到列出的伺服器，但它在呼叫之間是穩定的。  
  
列出的伺服器不一定含有 `IsClustered` 和版本等其他資訊。 這取決於清單的取得方式。 透過 SQL Server 瀏覽器服務列出的伺服器所具有的詳細資料，要多於透過 Windows 基礎結構找到的伺服器 (僅列出名稱)。  
  
> [!NOTE]
>  只有在完全信任中執行時，才可以使用伺服器列舉。 在部分信任的環境中執行的組件將無法使用它，即使它們具有 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 程式碼存取安全性 (CAS) 權限也一樣。  
  
SQL Server 可藉由使用名為 SQL Browser 的外部 Windows 服務來提供 <xref:System.Data.Sql.SqlDataSourceEnumerator> 相關資訊。 此服務預設會啟用，但系統管理員可能會將其關閉或停用，讓此類別看不到伺服器執行個體。  
  
## <a name="example"></a>範例  
下列主控台應用程式會擷取所有可見 SQL Server 執行個體的相關資訊，並在主控台視窗中顯示該資訊。  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
