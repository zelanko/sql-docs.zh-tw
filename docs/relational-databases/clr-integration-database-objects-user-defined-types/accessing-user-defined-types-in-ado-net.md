---
title: 存取 ADO.NET 中的使用者定義類型 |Microsoft Docs
description: 以 .NET Framework CLR 語言撰寫的 Udt，可讓 SQL Server 資料庫儲存物件和自訂資料結構。 在 ADO.NET 中，提供者會公開 Udt。
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488237"
---
# <a name="accessing-user-defined-types-in-adonet"></a>存取 ADO.NET 中的使用者定義型別
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用者定義類型（Udt）是使用產生可驗證程式代碼的[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework common language RUNTIME （CLR）所支援的任何語言所撰寫。 這包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic。 UDT 允許在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中儲存物件及自訂資料結構。 資料會做為 .NET Framework 類別或結構的公用成員而公開，行為可使用類別或結構的方法來定義。 UDT 可用作資料表的資料行定義、[!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中的變數，或是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函式或預存程序的引數。  
  
 在 ADO.NET 中， **SqlClient**提供者會以下列方式公開 udt：  
  
-   透過**SqlClient. SqlDataReader**做為物件。  
  
-   透過**SqlDataReader**的原始位元組。  
  
-   當做**SqlClient. SqlParameter**物件的參數。  
  
## <a name="in-this-section"></a>本節內容  
 [擷取 UDT 資料](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 說明如何擷取 UDT 資料及如何指定參數。  
  
 [以 DataAdapter 更新 UDT 資料行](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 描述如何在**資料集中**使用 udt，以及如何使用**dataadapter**更新 udt 資料。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
