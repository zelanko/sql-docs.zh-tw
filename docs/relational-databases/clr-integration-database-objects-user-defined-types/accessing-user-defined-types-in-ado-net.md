---
title: 存取ADO.NET的使用者定義類型 |微軟文件
description: 用 .NET 框架 CLR 語言編寫的 UDT 允許 SQL Server 資料庫儲存物件和自訂資料結構。 在ADO.NET,提供程式公開 UDT。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
ms.openlocfilehash: d14205a6fb506f5d4fddaac1ab601ff1ee9205b8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488237"
---
# <a name="accessing-user-defined-types-in-adonet"></a>存取 ADO.NET 中的使用者定義型別
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用者定義的類型 (UDT)[!INCLUDE[msCoName](../../includes/msconame-md.md)]使用 .NET Framework 通用語言執行時 (CLR) 支援的任何語言編寫,這些語言生成可驗證的代碼。 這包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic。 UDT 允許在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存物件及自訂資料結構。 資料會做為 .NET Framework 類別或結構的公用成員而公開，行為可使用類別或結構的方法來定義。 UDT 可用作資料表的資料行定義、[!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中的變數，或是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函式或預存程序的引數。  
  
 在**ADO.NET,System.Data.SqlClient**提供者以以下方式公開 UDT:  
  
-   通過**系統.Data.SqlClient.SqlDataReader**作為一個物件。  
  
-   通過**SqlDataReader**作為原始位元組。  
  
-   為**系統.Data.SqlClient.Sql參數物件的參數**。  
  
## <a name="in-this-section"></a>本節內容  
 [擷取 UDT 資料](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 說明如何擷取 UDT 資料及如何指定參數。  
  
 [以 DataAdapter 更新 UDT 資料行](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 介紹如何使用**DataSet**中的 UDT 以及如何使用**DataAdapter**更新 UDT 資料。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
