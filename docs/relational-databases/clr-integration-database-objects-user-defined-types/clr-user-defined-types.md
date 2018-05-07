---
title: CLR 使用者定義型別 |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- validation [CLR integration]
- types [CLR integration]
- UserDefined serialization format [CLR integration]
- null values [CLR integration]
- serialization
- Native serialization format [CLR integration]
- databases [CLR integration]
- building database objects [CLR integration], user-defined types
- user-defined types [CLR integration]
- common language runtime [SQL Server], user-defined types
- UDTs [CLR integration]
- database objects [CLR integration], user-defined types
- turning on CLR functionality
- customizing UDT expression return types [CLR integration]
- UDTs [CLR integration], about UDTs
- comparing UDT values
- annotations [CLR integration]
- user-defined types [CLR integration], about UDTs
- variables [CLR integration]
- invoking UDT methods
- indexes [CLR integration]
ms.assetid: 27c4889b-c543-47a8-a630-ad06804f92df
caps.latest.revision: 67
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 962f3ea6789f0a4dd9fa5ad6169801b3dd589223
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="clr-user-defined-types"></a>CLR 使用者定義型別
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供的功能可讓您建立針對 .NET Framework Common Language Runtime (CLR) 中建立的組件來進行程式設計的資料庫物件。 資料庫物件可充分運用 CLR 所提供的豐富程式設計模型，包括觸發程序、預存程序、函數、彙總函式和類型等。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，執行 CLR 程式碼的功能預設會設定為 OFF。 來啟用 CLR，請使用**sp_configure**系統預存程序。  
  
 開頭為[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，您可以使用使用者定義型別 (Udt) 來擴充伺服器的純量類型系統啟用 CLR 物件儲存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 UDT 可以包含多個元素並可以具有行為，使其有別於由單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型組成的傳統別名資料類型。  
  
 因為系統將 UDT 當做一個整體來進行存取，所以它們使用的複雜資料類型可能會對效能產生負面影響。 通常使用傳統資料列及資料表可以對複雜資料進行最佳模型化。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 UDT 適用於以下項目：  
  
-   日期、時間、貨幣及擴充的數值類型  
  
-   Geospatial 應用程式  
  
-   編碼或加密的資料  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中開發 UDT 的過程包含下列步驟：  
  
1.  **程式碼，並建立可定義 UDT 的組件。** UDT 是使用會產生可驗證程式碼之 .NET Framework Common Language Runtime (CLR) 支援的任何語言所定義。 這包括 Visual C# 和 Visual Basic .NET。 資料會公開為 .NET Framework 類別或結構的欄位及屬性，並且其行為是由類別或結構的方法所定義。  
  
2.  **註冊組件。** 可以透過 Visual Studio 使用者介面，在資料庫專案，或使用部署 Udt [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 陳述式，它將會複製到資料庫中包含的類別或結構的組件。  
  
3.  **在 SQL Server 中建立 UDT。** 一旦將組件載入主機資料庫，您會使用[!INCLUDE[tsql](../../includes/tsql-md.md)]CREATE TYPE 陳述式來建立 UDT，並公開為 UDT 的成員類別或結構的成員。 UDT 僅存在於單一資料庫的內容中，並且一旦註冊後，就不再與建立它們的外部檔案具有相依性。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前，不支援從 .NET Framework 組件建立的 UDT。 不過，您仍然可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]別名資料類型使用**sp_addtype**。 CREATE TYPE 語法可用來建立原生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者定義資料類型及 UDT。  
  
4.  **建立資料表、 變數或參數使用 UDT**開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，使用者定義型別可用做資料表的資料行定義中的變數[!INCLUDE[tsql](../../includes/tsql-md.md)]批次，或做為引數的[!INCLUDE[tsql](../../includes/tsql-md.md)]函式或預存程序。  
  
## <a name="in-this-section"></a>本節內容  
 [建立使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
 描述如何建立 UDT。  
  
 [在 SQL Server 中註冊使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/registering-user-defined-types-in-sql-server.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中註冊及管理 UDT。  
  
 [使用 SQL Server 中的 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
 描述如何使用 UDT 建立查詢。  
  
 [存取 ADO.NET 中的使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-in-ado-net.md)  
 描述如何在 ADO.NET 中，使用 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來處理 UDT。  
  
  
