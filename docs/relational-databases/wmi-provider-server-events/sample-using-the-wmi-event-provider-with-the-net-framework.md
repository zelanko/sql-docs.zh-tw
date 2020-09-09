---
title: 範例：在 .NET 中使用 WMI 事件提供者
description: '範例 c # 應用程式會使用 WMI 事件提供者，針對 SQL Server 實例上發生的所有資料定義語言事件傳回事件資料。'
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Server Events, samples
- sample applications [WMI]
- managed code [WMI]
ms.assetid: 3d7aa7e9-0bb3-4a5b-9a3c-047f3240a6f8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ac51d05e79b11f35b264db4f23e5107f8de89b97
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539934"
---
# <a name="sample-using-the-wmi-event-provider-with-the-net-framework"></a>範例：搭配 .NET Framework 使用 WMI 事件提供者
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  下列範例會以 C# 建立應用程式，這個應用程式會使用 WMI 事件提供者，針對在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設安裝執行個體上發生的所有資料定義語言 (DDL) 事件傳回事件資料。  
  
## <a name="example"></a>範例  
 此範例會使用下列命令檔進行編譯：  
  
```  
set compiler_path=C:\WINNT\Microsoft.NET\Framework\v2.0.50110  
  
%compiler_path%\csc %1  
```  
  
```  
using System;  
using System.Management;  
  
class SQLWEPExample   
{  
    public static void Main(string[] args)  
    {  
        string query =  @"SELECT * FROM DDL_EVENTS " ;  
        // Default namespace for default instance of SQL Server   
        string managementPath =  
            @"\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER";  
        ManagementEventWatcher  watcher =   
            new ManagementEventWatcher(new WqlEventQuery (query));  
        ManagementScope scope = new ManagementScope (managementPath);  
        scope.Connect();  
        watcher.Scope = scope;  
        Console.WriteLine("Watching...");  
        while (true)  
        {  
            ManagementBaseObject obj = watcher.WaitForNextEvent();  
            Console.WriteLine("Event!");  
            foreach (PropertyData data in obj.Properties)  
            {  
                Console.Write("{0}:", data.Name);  
                if (data.Value == null)  
                {  
                    Console.WriteLine("<null>");  
                }  
                else  
                {  
                    Console.WriteLine(data.Value.ToString());  
                }  
            }  
            Console.WriteLine("-----");  
            Console.WriteLine();  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [伺服器事件的 WMI 提供者概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
